# FUN WITH GO

![Golang](golang.webp)

## INTRODUCTION

Are you looking for a Swiss Army Knife to add to your toolbox? Here you GO! From creating Web Applications to writing scripts, handling micro-controllers, and the ability of GO to compile on nearly any machine. GO is a true definition of a Swiss Army Knife Coming from a scripting background myself, I've used python for most of my scripting, I decided to try out Golang for an operation I had written in python and it's safe to say I'm impressed and a Gopher now. This article will look at using Go slices where we create, read, update and delete entries we are calling thoughts. Let's call the program "ThoughtBox".

## IMPORTANT!

- We are taking the learn-by-doing approach, for Go fundamentals visit the official Go [docs](https://www.genome.gov/).

- This is a command line program.

- We are not working with a database, third-party libraries, or custom packages.

- You can clone the repo on GitHub[Github Repository](https://github.com/WatipasoChirambo/GO-Thought-Box).

## PREREQUISITES

- Basic programming knowledge.
- Familiarity with Go
- GO installed
- Basic command line knowledge
- IDE or TextEditor of your choice. "I'm using vscode"

## LET'S GO!

### FIRST STEPS

- Create a folder for our project, and name it whatever you like.
- Create a file named main.go in our project folder.

To start, open main.go file. Inside the file let's have the following pieces of code.

```Golang
package main

import (
	"bufio"
	"fmt"
	"os"
)

type Thought struct {
	title string
}

func main() {
	thoughts := []Thought{
		{
			title: "Learn Go",
		},
		{
			title: "Buy new machine",
		},
		{
			title: "create a JavaScript TwitterBot",
		},
	}
}
```

At the top of our code snippet, we have package main which tells the GO compiler that the package should compile the written program as an executable.
Below the package main line, we have our imports, for our project we have a few imports, it's a small program.
Below our imports, we have our Struct which is similar to a class if you are familiar with other programming languages like Python, C#, and Java.
The entry point of our program is the main function, which we have below our Struct.

\*NOTE!

Functions are declared using the func keyword\*.

```Golang
package main

import (
	"bufio"
	"fmt"
	"os"
)

type Thought struct {
	title string
}

func main() {
	thoughts := []Thought{
		{
			title: "Learn Go",
		},
		{
			title: "Buy new machine",
		},
		{
			title: "create a JavaScript TwitterBot",
		},
	}
    fmt.Println(thoughts) //add this
}
```

Inside the main function, we are creating a slice of type Thought and adding three thoughts to our struct. We are then printing our slice of thoughts with the Golang built-in fmt module.



## CREATE THOUGHT

Let the fun begin. Let's create a function that handles the creation of a single thought and adds it to our slice"ThoughtBox".

```Golang
func CreateThought(thoughts *[]Thought) {
	inputReader := bufio.NewReader(os.Stdin)
	fmt.Println("Add a thought: ")
	userInput, _ := inputReader.ReadString('\n')
	thought := Thought{title: userInput}
	*thoughts = append(*thoughts, thought)
	fmt.Println("Thought added successfully")
}
```

In the code snippet above, we defined our function that takes one argument which is a slice of type Thought.
There are a couple of ways to obtain user input, in our case, we are using Golangs built-in bufio module. Since a single thought can have a space or more in between words, we are keeping all that input including spaces no matter the thought and to do that we are using Golangs built-in bufio module.
We first prompt the user to Add a thought, when the user enters a thought we append(add) it to the slice of thoughts using the append slice method.
After user input is successful we print out that the thought was added successfully.

## READING THOUGHTS
Since we are able to add thoughts, let's look at how we can get our thoughts from our thoughtbox.

## READ SINGLE THOUGHT
Since we are able to add thoughts, let's look at how we can get our thoughts from our thoughtbox.

```Golang
func GetThought(thoughts []Thought, thoughtId int) string {
	for index, _ := range thoughts {
		if index+1 == thoughtId {
			return thoughts[index].title
		}
	}
	return "thought not available"
}
```

### READ ALL
In order to get all thoughts in our box, we need to loop through all our elements and print all thoughts we have. The code snippet below does exactly what we've just discussed.

```Golang
func ReadAllThoughts(thoughts []Thought) {
	for _, thought := range thoughts {
		fmt.Println(thought.title)
	}
}
```

## UPDATE THOUGHT
The update function takes in three arguments, the slice of type Thought., user Input text, which modifies the element that has been chosen. Below is our code snippet.


```Golang
func UpdateThought(thoughts []Thought, thoughtId int, newThought string) {
	for index, _ := range thoughts {
		if index+1 == thoughtId {
			(thoughts)[index].title = newThought
			fmt.Println("Thought updated successfully")
			return
		}
	}
}
```

## DELETE THOUGHT
The Delete function takes in two arguments, the slice of type Thought and a thought id, which modifies the element that has been chosen. Below is our code snippet.

```Golang
func DelThought(thoughts []Thought, thoughtId int) {
	for index, _ := range thoughts {
		if index+1 == thoughtId {
			thoughts = append((thoughts)[:index], (thoughts)[index+1:]...)
			return
		}
	}
}
```

## FULL PROJECT

```
package main

import (
	"bufio"
	"fmt"
	"os"
)

type Thought struct {
	title string
}

func main() {
	thoughts := []Thought{
		{
			title: "Learn Go",
		},
		{
			title: "Buy new machine",
		},
		{
			title: "create a JavaScript TwitterBot",
		},
	}
	CreateThought(&thoughts)
	ReadAllThoughts(thoughts)
	DelThought(thoughts, 2)
	UpdateThought(thoughts, 1, "Rokka")
	GetThought(thoughts,1)
}

// CREATE THOUGHT
func CreateThought(thoughts *[]Thought) {
	inputReader := bufio.NewReader(os.Stdin)
	fmt.Println("Add a thought: ")
	userInput, _ := inputReader.ReadString('\n')
	thought := Thought{title: userInput}
	*thoughts = append(*thoughts, thought)
	fmt.Println("Thought added successfully")
}

// GET THOUGHT
func GetThought(thoughts []Thought, thoughtId int) string {
	for index, _ := range thoughts {
		if index+1 == thoughtId {
			return thoughts[index].title
		}
	}
	return "thought not available"
}

// DELETE ENTRIES
func DelThought(thoughts []Thought, thoughtId int) {
	for index, _ := range thoughts {
		if index+1 == thoughtId {
			thoughts = append((thoughts)[:index], (thoughts)[index+1:]...)
			return
		}
	}
}

func UpdateThought(thoughts []Thought, thoughtId int, newThought string) {
	for index, _ := range thoughts {
		if index+1 == thoughtId {
			(thoughts)[index].title = newThought
			fmt.Println("Thought updated successfully")
			return
		}
	}
}

func ReadAllThoughts(thoughts []Thought) {
	for _, thought := range thoughts {
		fmt.Println(thought.title)
	}
}
```

## CONCLUSION
I believe going through this write up you are able to write a program in GO. We are more than willing to guide you into becoming a Gopher! Let’s get creative and transform the world in all possible ways, The GO way

