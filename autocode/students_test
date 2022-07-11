package coverage_test

import (
	"coverage"
	"errors"
	"fmt"
	"os"
	"reflect"
	"testing"
	"time"
)

// DO NOT EDIT THIS FUNCTION
func init() {
	content, err := os.ReadFile("students_test.go")
	if err != nil {
		panic(err)
	}
	err = os.WriteFile("autocode/students_test", content, 0644)
	if err != nil {
		panic(err)
	}
}

// WRITE YOUR CODE BELOW
//go test -v -coverprofile=/covered
//go tool cover -html=covered

func TestPeople_Len(t *testing.T) {
	family := coverage.People{coverage.Person{}, coverage.Person{}, coverage.Person{}}
	peopleCount := family.Len()
	if peopleCount != 3 {
		t.Errorf("Oops: %d", errors.New("people amount is invalid"))
	}
}

var date0, _ = time.Parse("2006-01-02", "2006-01-02")
var person0 = coverage.NewPerson("Igor", "Nikolaev", date0)
var date1, _ = time.Parse("2006-01-02", "2006-01-02")

func TestPeople_Less_Birthday(t *testing.T) {
	date1, _ := time.Parse("2006-01-02", "2006-01-01")
	person1 := coverage.NewPerson("Igor", "Nikolaev", date1)
	friends := coverage.People{person0, person1}

	needSwap := friends.Less(0, 1)
	if !needSwap {
		t.Errorf("People_Less crashed: %d", errors.New("first date is bigger"))
	}
}

func TestPeople_Less_FirstName(t *testing.T) {
	person1 := coverage.NewPerson("Ivan", "Nikolaev", date1)
	friends := coverage.People{person0, person1}

	needSwap := friends.Less(0, 1)
	if !needSwap {
		t.Errorf("People_Less crashed: %d", errors.New("first firstname is bigger"))
	}
}

func TestPeople_Less_LastName(t *testing.T) {
	person0 = coverage.NewPerson("Igor", "Andreev", date0)
	person1 := coverage.NewPerson("Igor", "Nikolaev", date1)
	friends := coverage.People{person0, person1}

	needSwap := friends.Less(0, 1)
	if !needSwap {
		t.Errorf("People_Less crashed: %d", errors.New("first lastname is bigger"))
	}
}

func TestPeople_Swap(t *testing.T) {
	person1 := coverage.NewPerson("Ivan", "Nikolaev", date1)
	friends := coverage.People{person0, person1}

	friends.Swap(0, 1)
	if friends[0] != person1 || friends[1] != person0 {
		t.Errorf("People_Swap crashed: %d", errors.New("people hasn't swapped"))
	}
}

/////////////////////////////////////////////////////////////////////////////////////////////////////

func TestMatrix_New(t *testing.T) {
	matrixStr := "1 2 3\n4 5 6\n7 8 9"
	_, err := coverage.New(matrixStr)
	if err != nil {
		t.Errorf("MatrixNew error: %d", errors.New("failed to create matrix"))
	}
}

func TestMatrix_New_InvalidRowsLength(t *testing.T) {
	matrixStr := "1 2 3\n4 5 6 4 6\n7 8 9"
	_, err := coverage.New(matrixStr)
	if !errors.As(fmt.Errorf("Rows need to be the same length"), &err) {
		t.Errorf("MatrixNew error: able to matrix with differrent rows length")
	}
}

func TestMatrix_New_InvalidData(t *testing.T) {
	matrixStr := "A 2 3\n4 5 6\n7 8 9"
	_, err := coverage.New(matrixStr)
	if err == fmt.Errorf("Rows need to be the same length") || err == nil {
		t.Errorf("MatrixNew error: %d", errors.New("able to matrix with differrent rows length"))
	}
}

func TestMatrix_Rows(t *testing.T) {
	matrixStr := "1 2 3\n4 5 6\n7 8 9"
	matrix, _ := coverage.New(matrixStr)

	rows := matrix.Rows()
	rowsCorrect := [][]int{[]int{1, 2, 3}, []int{4, 5, 6}, []int{7, 8, 9}}
	if !reflect.DeepEqual(rows, rowsCorrect)  {
		t.Errorf("incorrect matrix rows slice")
	}

}

func TestMatrix_Cols(t *testing.T) {
	matrixStr := "1 2 3\n4 5 6\n7 8 9"
	matrix, _ := coverage.New(matrixStr)

	cols := matrix.Cols()
	colsCorrect := [][]int{[]int{1, 4, 7}, []int{2, 5, 8}, []int{3, 6, 9}}
	if !reflect.DeepEqual(cols, colsCorrect)  {
		t.Errorf("incorrect matrix cols slice")
	}
}

func TestMatrix_Set(t *testing.T) {
	matrixStr := "1 2 3\n4 5 6\n7 8 9"
	matrix, _ := coverage.New(matrixStr)
	setSuccess := matrix.Set(0, 0, 10)
	if !setSuccess {
		t.Errorf("matrix set ended success with wrong indices")
	}
}

func TestMatrix_Set_False(t *testing.T) {
	matrixStr := "1 2 3\n4 5 6\n7 8 9"
	matrix, _ := coverage.New(matrixStr)
	setSuccess := matrix.Set(-1, 0, 10)
	if setSuccess {
		t.Errorf("matrix set ended success with wrong indices")
	}
}
