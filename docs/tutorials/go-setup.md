# Setting up a Dev container for Go

* Primary author: [Baotran Nguyen](https://github.com/bnln7)
* Reviewer: [Paige Pan](https://github.com/ppan1229)

## Introduction
Here is a tutorial on setting up a new DevContainer project for the Go programming language. 

!!! note
    Many instructions reused from 423 MkDocs tutorial.


## Prerequisites
1. Github account: Create one [here](https://github.com/).
2. Git: Install it [here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
3. Docker: Install it [here](https://www.docker.com/products/docker-desktop).
4. Command Terminal
5. A tool to edit your code. In this tutorial, we will use VS Code (download [here](https://code.visualstudio.com/)).

## Git Repo Set-Up
### Create a Local Directory and Initialize Git
1. Open your terminal or command prompt. 
2. Create a new directory for your project:
```go
mkdir <name of directory>
cd <name of directory>
```
For the purposes of this tutorial, the name of the directory will be "hello" and will be referred to as such. Example:
```go
mkdir hello
cd hello
```
3. Initialize a new Git repository:
```go
git init
```
4. Create a README file:
```go
echo "[Go Tutorial](https://<your-github-username-here>.github.io/comp423-course-notes/tutorials/go-setup/)">README.md
echo "Navigate to tutorials in the menu on the website to see the Go Tutorial if necessary.">>README.md
git add README.md
git commit -m "Initial commit with README"

```
### Create a Remote Repository on Github
1. Log in to your Github account and navigate to the [Create a New Repository](https://github.com/new) page.
2. Fill in the details as follows:

    * Repository Name: `go-hello-world-project`
    * Description: "Hello World Go Program"
    * Visibility: Public
    * Click `Create Repository`

### Link your Local Repository Github
1. In your terminal, add the Github repository as a remote:
```go
git remote add origin https://github.com/<your-username>/go-hello-world-project.git
```
Replace `<your-username>` with your GitHub username.

2. Check your default branch name with the subcommand `git branch`. If it's not `main`, rename it to `main` with the following command: `git branch -M main`. 
```go
git push --set-upstream origin main
```



## Creating a New Dev Container
### Add Development Container Configuration
1. Open Docker and then open VS Code. In VS Code, open the `hello` directory. You can do this via: File > Open Folder.
2. Install the **Dev Containers** extension for VS Code. Do so by navigating to the left side and clicking the option with the 4 squares (the extensions option). In the search bar, type Dev Containers. Of the options that appear, click install for the one that says "Dev Containers" by Microsoft.
3. At the root of the project (`hello`), create a new directory labelled `.devcontainer`. Inside this newly created directory, create a new file labelled `devcontainer.json`. The `devcontainer.json` file defines the configuration for your development environment. In this file, write the following to create the correct environment for your program.
```go
{
  "name": "Go Hello World Project",
  "image": "mcr.microsoft.com/vscode/devcontainers/go:latest",
  "customizations": {
    "vscode": {
      "settings": {},
      "extensions": ["golang.go"]
    }
  },
  "postCreateCommand": "go version"
}
```
`devcontainer.json` files follow the above format.
    * `name` names the dev container. This name can be seen when the dev container is running.
    * `image` indicates the development environment that will be used
    * `extensions` installs the necessary extensions inside the dev container for the correct environment
    * `postCreateCommand` runs the specified command right after the dev container is created
4. Reopen the project in a VSCode Dev Container by pressing `Ctrl+Shift+P` or `Cmd+Shift+P`. Wait for everything to be installed. It should be finished when you see a message in the terminal asking you to press any button to terminate. Once you see the message, press any button or open a new terminal. 
5. Running
```
go version
```
should check that recent version of Go is being used.

## Initializing/Doing the Project
1. Change to the directory you created if not already in it. Type 
```go
pwd
```
into the terminal to check. If the end of the output is not the name of your directory, change directories. For example, if you are in the parent directory of `hello`, you would type:
Example:
```go
cd hello
```


2. Enable dependency tracking for your code by typing this in the terminal of your editor:
```go
go mod init example/hello
```
Doing so should result in this output:
```go
go: creating new go.mod: module example/hello
```

3. In your `hello` directory, create a new file labelled `hello.go`. This file will be where you write your code. 

4. In `hello.go`, type or paste this in and save the file.
```go
package main

import "fmt"

func main() {
    fmt.Println("Hello COMP423")
}
```

5. Run your code with this command:
```go
go run .
```
Example output:
```go
Hello COMP423
```

6. Make this into an executable using the build subcommand.
```go
go build hello.go
```
Running the built binary: Calling run just executes the program. In contrast, the build command makes the program into an executable. This executable can then be run. Just like the gcc command in the C programming language, the go build command in Go turns the file into an executable. Just like C, it can also then be run by typing
!!! note
    mac/linux
```go
./hello
```

## Final Steps: Pushing to a Repo
1. In your terminal, type
```go
git add .
git commit -m "Final Hello World Project"
git push -u origin main
```

Congratulations! You are done!