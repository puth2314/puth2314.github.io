---
title: "Learnings: Go"
date: 2025-04-14 10:00:00 +0700
description: Notes from learning Go.
categories: [Software, Language]
tags: [learnings, go, golang]
---


<!-- 
https://youtu.be/LHhsNa_Kgns?si=ssZB6Fs3Rus2kr5R

https://www.youtube.com/watch?v=gXmznGEW9vo&t=218s

https://www.youtube.com/watch?v=jFfo23yIWac&t=60s
https://github.com/AkhilSharma90/simple-http-server-GO

https://www.youtube.com/watch?v=un6ZyFkqFKo&t=27617s
https://github.com/bootdotdev/fcc-learn-golang-assets/blob/main/project/2-boilerplate/src/main.go

https://www.youtube.com/watch?v=h3fqD6IprIA&t=94s
https://github.com/sikozonpc/GopherSocial

https://www.youtube.com/watch?v=LHhsNa_Kgns
https://github.com/techwithtim/Go-API-Tutorial/blob/main/main.go 

https://puthearathaim.postman.co/workspace/812f78a5-e533-47fb-81d9-c1414aaaf53d/team-quickstart
-->


## Workflow

1. `go mod init github.com/your-username/your-repository`
   - This ... 
2. `go build .` or `go run .`
   - The former to compile your package to a binary.
   - The latter to both compile and then run the binary.


## Examples

<details>
<summary>Variables</summary>

```go
package main

import (
	"errors"
	"fmt"
	"unicode/utf8"
)

func main() {
	var intNum int = 32767
	intNum = intNum + 1
	fmt.Println(intNum)

	var floatNum float64 = 12345678.9
	fmt.Println(floatNum)

	var floatNum32 float32 = 10.1
	var intNum32 int32 = 2
	var result float32 = floatNum32 + float32(intNum32)
	fmt.Println(result)

	var intNum1 int = 3
	var intNum2 int = 2
	fmt.Println(intNum1 / intNum2)
	fmt.Println(intNum1 % intNum2)

	var myString string = "Hello" + " " + "World"
	fmt.Println(myString)

	fmt.Println(utf8.RuneCountInString("y"))

	var myRune rune = 'a'
	fmt.Println(myRune)

	var myBoolean bool = false
	fmt.Println(myBoolean)

	var intNum3 int
	fmt.Println(intNum3)

	var myVar string = foo()
	fmt.Println(myVar)

	var1, var2 := 1, 2
	fmt.Println(var1, var2)

	const myConst string = "const value"
	fmt.Println(myConst)

	const pi float32 = 3.1415

	var printValue string = "Hello World"
	printMe(printValue)

	var numerator int = 11
	var denominator int = 0
	var result, remainder, err = intDivision(numerator, denominator)
	switch {
	case err != nil:
		fmt.Printf(err.Error())
	case remainder == 0:
		fmt.Printf("The result of the integer division is %v", result)
	default:
		fmt.Printf("The result of the integer division is %v with remainder %v", result, remainder)
	}
	switch remainder {
	case 0:
		fmt.Println("The dvision was exact")
	case 1, 2:
		fmt.Println("The division was close")
	default:
		fmt.Printf("The division was not close")
	}

	intArr := [...]int32{1, 2, 3}
	fmt.Println(intArr)

	var intSlice []int32 = []int32{4, 5, 6}
	fmt.Printf("The length is %v with capacity %v", len(intSlice), cap(intSlice))
	intSlice = append(intSlice, 7)
	fmt.Printf("\nThe length is %v with capacity %v\n", len(intSlice), cap(intSlice))

	var intSlice2 []int32 = []int32{8, 9}
	intSlice = append(intSlice, intSlice2...)
	fmt.Println(intSlice)

	var intSlice3 []int32 = make([]int32, 3, 10)
	fmt.Println(intSlice3)

	var myMap map[string]uint8 = make(map[string]uint8)
	fmt.Println(myMap)

	var myMap2 = map[string]uint8{"Adam": 23, "Sarah": 45}
	fmt.Println(myMap2["Adam"])
	var age, ok = myMap2["Jason"]
	if ok {
		fmt.Printf("The age is %v", age)
	} else {
		fmt.Printf("Invalid Name")
	}

	for name, age := range myMap2 {
		fmt.Printf("Name: %v, Age: %v \n", name, age)
	}

	for i, v := range intArr {
		fmt.Printf("Index: %v, Value: %v \n", i, v)
	}

	for i := 0; i < 10; i++ {
		fmt.Println(i)
	}


	var myString = []rune["resume"]
	var indexed = myString[1]
	fmt.Printf("%v, %T\n", indexed, indexed)
	for i, v := range myString {
		fmt.Println(i, v)
	}
	fmt.Printf("\nThe length of 'myString' is %v", len(myString))

	var myRune = 'a'
	fmt.Printf("\nmyRune = %v", myRune)

	var strSlice = []string{"s", "u", "b", "s", "c", "r", "i", "b", "e"}
	var catStr = ""
	for i := range strSlice {
		catStr += strSlice[i]
	}
	fmt.Printf("\n%v", catStr)
}

func printMe(printValue string) {
	fmt.Println(printValue)
}

func intDivision(numerator int, denominator int) (int, int, error) {
	var err error
	if denominator == 0 {
		err = errors.New("Cannot Divide by Zero")
		return 0, 0, err
	}
	var result int = numerator / denominator
	var remainder int = numerator % denominator
	return result, remainder, err
}
```

</details>

<details>
<summary>Structs</summary>

```go
package main

import "fmt"

type gasEngine struct {
	mpg     uint8
	gallons uint8
	owner
	int
}

type owner struct {
	name string
}

type electricEngine struct {
	mpkwh uint8
	kwh   uint8
}

func (e gasEngine) milesLeft() uint8 {
	return e.gallons * e.mpg
}

func (e electricEngine) milesLeft() uint8 {
	return e.kwh * e.mpkwh
}

type engine interface {
	milesLeft() uint8
}

func canMakeit(e engine, miles uint8) {
	if miles <= e.milesLeft() {
		fmt.Println("You can make it there!")
	} else {
		fmt.Println("Need to fuel up first!")
	}
}

func main() {
	var myEngine gasEngine = gasEngine{25, 15, owner{"Alex"}, 10}
	fmt.Println(myEngine.mpg, myEngine.gallons, myEngine.name)
	canMakeit(myEngine, 50)
	fmt.Printf("Total miles left in tank: %v", myEngine.milesLeft())
	var myEngine2 electricEngine = electricEngine{25, 15}
	canMakeit(myEngine2, 50)
}
```

</details>

<details>
<summary>Pointers</summary>

```go
package main

import (
	"fmt"
)

func main0() {
	var p *int32 = new(int32)
	var i int32
	fmt.Printf("The value p points to is: %v", *p)
	fmt.Printf("\nThe value if i is: %v", i)
	p = &i
	*p = i
	fmt.Printf("\nThe value p points to is: %v", *p)
	fmt.Printf("\nThe value if i is: %v", i)
	var k int32 = 2
	i = k
}

func main1() {
	var slice = []int32{1, 2, 3}
	var sliceCopy = slice
	sliceCopy[2] = 4
	fmt.Println(slice)
	fmt.Println(sliceCopy)
}

func main() {
	var thing1 = [5]float64{1, 2, 3, 4, 5}
	fmt.Printf("\nThe memory location of the thing1 array is: %p", &thing1)
	var result [5]float64 = square(&thing1)
	fmt.Printf("\nThe result is: %v", result)
	fmt.Printf("\nThe value of thing1 is: %v", thing1)
}

func square(thing2 *[5]float64) [5]float64 {
	fmt.Printf("\nThe memory location of the thing2 array is: %p", &thing2)
	for i := range thing2 {
		thing2[i] = thing2[i] * thing2[i]
	}
	return *thing2
}
```

</details>

<details>
<summary>Goroutines</summary>

```go
package main

import (
	"fmt"
	"sync"
	"time"
)

var m = sync.RWMutex{}
var wg = sync.WaitGroup{}
var dbData = []string{"id1", "id2", "id3", "id4", "id5"}
var results = []string{}

func main() {
	t0 := time.Now()
	for i := 0; i < len(dbData); i++ {
		wg.Add(1)
		go dbCall(i)
	}
	wg.Wait()
	fmt.Printf("\nTotal execution time: %v", time.Since(t0))
	fmt.Printf("\nThe results are %v", results)
}

func dbCall(i int) {
	var delay float32 = 2000
	time.Sleep(time.Duration(delay) * time.Millisecond)
	fmt.Println("The result from the database is:", dbData[i])
	save(dbData[i])
	log()
	wg.Done()
}

func save(result string) {
	m.Lock()
	results = append(results, dbData[i])
	m.Unlock()
}

func log() {
	m.RLock()
	fmt.Printf("\nThe current results are: %v", results)
	m.RUnlock()
}
```

</details>

<details>
<summary>Channels</summary>

```go
package main

import (
	"fmt"
	"math/rand/v2"
	"time"
)

var MAX_CHICKEN_PRICE float32 = 5
var MAX_TOFU_PRICE float32 = 3

func main4() {
	var chickenChannel = make(chan string)
	var tofuChannel = make(chan string)
	var websites = []string{"walmart.com", "costco.com", "wholefoods.com"}
	for i := range websites {
		go checkChickenPrices(websites[i], chickenChannel)
		go checkTofuPrices(websites[i], tofuChannel)
	}
	sendMessage(chickenChannel, tofuChannel)
}

func checkTofuPrices(website string, c chan string) {
	for {
		time.Sleep(time.Second * 1)
		var tofu_price = rand.Float32() * 20
		if tofu_price < MAX_TOFU_PRICE {
			c <- website
			break
		}
	}
}
func checkChickenPrices(website string, chickenChannel chan string) {
	for {
		time.Sleep(time.Second * 1)
		var chickenPrice = rand.Float32() * 20
		if chickenPrice <= MAX_CHICKEN_PRICE {
			chickenChannel <- website
			break
		}
	}
}

func sendMessage(chickenChannel chan string, tofuChannel chan string) {
	select {
	case website := <-chickenChannel:
		fmt.Printf("\nFound a deal on chicken at %v.", website)
	case website := <-tofuChannel:
		fmt.Printf("\nEmail Sent: Found deal on tofu at %v.", website)
	}
}

func main3() {
	var c = make(chan int, 5)
	go process(c)
	for i := range c {
		fmt.Println(i)
		time.Sleep(time.Second * 1)
	}
}

func process(c chan int) {
	defer close(c)
	for i := 0; i < 5; i++ {
		c <- i
	}
	fmt.Println("Exiting process")
}
```

</details>

<details>
<summary>Generics</summary>

```go
package main

import (
	"encoding/json"
	"fmt"
	"io/ioutil"
)

type contactInfo struct {
	Name  string
	Email string
}

type purchaseInfo struct {
	Name   string
	Price  float32
	Amount int
}

func main() {
	var contacts []contactInfo = loadJSON[contactInfo]("./contactInfo.json")
	fmt.Printf("\n%+v", contacts)

	var purchases []purchaseInfo = loadJSON[purchaseInfo]("./purchaseInfo.json")
	fmt.Printf("\n%+v", purchases)
}

func loadJSON[T contactInfo | purchaseInfo](filePath string) []T {
	data, _ := ioutil.ReadFile(filePath)

	var loaded = []T{}
	json.Unmarshal(data, &loaded)

	return loaded
}

func main() {
	var intSlice = []int{1, 2, 3}
	fmt.Println(sumSlice[int](intSlice))

	var float32Slice = []float32{1, 2, 3}
	fmt.Println(sumSlice[float32](float32Slice))
}

func sumSlice[T int | float32 | float64](slice []T) T {
	var sum T
	for _, v := range slice {
		sum += v
	}
	return sum
}

func main() {
	var intSlice = []int{}
	fmt.Println(isEmpty(intSlice))

	var float32Slice = []float32{1, 2, 3}
	fmt.Println(isEmpty(float32Slice))
}

func isEmpty[T any](slice []T) bool {
	return len(slice) == 0
}
```

</details>


## Resources

- [A Tour of Go](https://go.dev/tour/list)
- [Go by Example](https://gobyexample.com/)
- [Effective Go](https://go.dev/doc/effective_go)
- [Let's Go](https://lets-go.alexedwards.net/)
