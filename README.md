# const2map
A Go tool to auto generate reflective maps for your enums

## Fork

This is a fork of [stringer](https://github.com/golang/tools/tree/master/cmd/stringer)
changed to generate a map of names and values instead of `String() string`.

The purpose is to workaround missing reflection capabilities to access constants names.

## Installation

```
go get github.com/vearutop/go-const2map
```

## Usage

Having `day.go` with this contents:

```go
//go:generate const2map -type=Day

type Day int
const (
	Monday Day = iota
	Tuesday
	Wednesday
	Thursday
	Friday
	Saturday
	Sunday
)
```

After running `go generate` you will get `day_c2m_gen.go`

```
const _Day_name = "MondayTuesdayWednesdayThursdayFridaySaturdaySunday"

var _Day_map = map[Day]string{
	0: _Day_name[0:6],
	1: _Day_name[6:13],
	2: _Day_name[13:22],
	3: _Day_name[22:30],
	4: _Day_name[30:36],
	5: _Day_name[36:44],
	6: _Day_name[44:50],
}

func (i Day) GetMap() map[Day]string {
	return _Day_map
}
```