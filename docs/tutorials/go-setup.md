# Setting up a dev container for Go 

* Primary author: [Wai Phyo Hein](https://github.com/waiphyo04)
* Reviewer: [Lingxiao Han](https://github.com/Lingxiao-Han)

## Installing required software
1. Install Git: [Git](https://git-scm.com/downloads)
2. Setup [Github](https://github.com/) account 
3. Install Visual Studio Code: [VS Code](https://code.visualstudio.com/download)
4. Install Docker: [Docker](https://www.docker.com/get-started/)
5. Understand Command Line Basics: [Mac](https://github.com/0nn0/terminal-mac-cheatsheet?tab=readme-ov-file#english-version) [Window](https://sansorg.egnyte.com/dl/AvZo1dS7kI)

## Setting up the developer environment
# Setting up Git
1. Open terminal on your local device and navigate to the file directory you want to start this project or you can use the following command in the terminal to create a new directory
```bash
mkdir <your preferred directory name>
cd <the directory name you just created above
```
2. Initialize the git repository with the following command 
```bash
git init
```
3. Create a README file
```bash
echo "# Go programming language" > README.md
git add README.md
git commit -m "Initial commit with README"
```
# Setting up a Remote Repository on Github
1. Log in to your [Github](https://github.com/) and create a **new repository**. 

2. Fill in the details as follows
    - **Repository Name:** `Go Programming Language Tutorial`
    - **Description:** "A basic coding project in rust language"
    - **Visibility:** Public
3. Do not initialize the repository with a README, .gitignore, or license.
4. Click **Create Repository**

# Link your local repository to Github
1. Add a GitHub repository as a remote:
```bash
git remote add origin https://github.com/<your-usernmae>/<your-directory-name>
```
remember to replace "<your-usernmae>" and "<your-directory-name>" with your actual GitHub username.

2. Check your default branch name 
```bash
git branch
```
The default name must be `main`. If it is not `main`, run the following command. 
```bash
git branch -M main
```
3. Push your local commits to the Github repository
```bash
git push --set-upstream origin main
```
!!! What is --set-upsteam

    `git push --set-upstream origin main`: This command pushes the main branch to the remote repository origin. The `--set-upstream` flag sets up the main branch to track the remote branch, meaning future pushes and pulls can be done without specifying the branch name and just writing git push origin when working on your local main branch. This long flag has a corresponding `-u` short flag.
    
4. Refresh the Github Repository page in your browser to make sure you see the commit you made recently. `git log` can be used locally to see commit ID and messages. 

## Setting up the Development Environment
1. In VS code, open the directory you created for this tutorial. 
2. Install **Dev Containers** extension in VS code. 
3. Create a `.devcontainer` directory in the root of your project with the following file inside of this "hidden" configuration directory. `.devcontainer/devcontainer.json`

The devcontainer.json file defines the configuration for your development environment. Here, we're specifying the following:

- **name:** A descriptive name for your dev container
- **image:** The Docker image to use, in this case, the latest version of a Python environment. [You can find many Docker image in this Microsoft page](https://hub.docker.com/r/microsoft/vscode-devcontainers)
- **customizations**:  
  - **vscode**: These settings enhance the VS Code experience within the container.  
    - **settings**: Customize VS Code editor settings for this project.
    - **extensions**: This indicates any VS Code extension that we want to include in this container. In this case, we includes the `golang.go` extension.
- **postCreateCommand:** A command to run after the container is created. `go mod init hello-world` 
Please include the following code in the .devcontainer.json file. 
```json
{
    "name": "go-project",
    "image": "mcr.microsoft.com/devcontainers/go:latest",
    "customizations": {
      "vscode": {
        "settings": {},
        "extensions": ["golang.go"]
      }
    },
    "postCreateCommand": "go mod init <your directory> "
  }
  ```
4. Reopen the project in VS code Dev Container by pressing `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac), typing `Dev Containers: Reopen in Container,` and selecting the option. Then choose `Go` for `Add Dev Container Configuration FIles`. Choose version `1.23-bookworm` and click `ok`. This may take a few minutes while the image is downloaded and the requirements are installed.

Once your dev container setup completes, close the current terminal tab (trash can), open a new terminal pane within VSCode, and try running `go version` to see your dev container is running a recent version of Go. 

In the root directory, make sure `go.mod` file exists. If you cannot find `go.mod` file, run 
```bash
go mod init github.com/<your_username>/<your-project-name>
```
Once it is created, enter into the file and check if the followign code exists. 
```bash
module go-tutorial
go 1.23.4
```
To see the Go version, run 
```bash
go version
```
It must show something similar to 1.23.4 which is a recent version of Go. 
## Running your first Go project
1. Create a file with your preferred name. The file name must be ended with `.go` to specify the file type. 
2. Type the following code snippet in your newly created file. 
```bash
package main

import "fmt"

func main() {
	fmt.Println("Hello COMP423")
}
```
3. In your terminal (it should be in your current directory), run the following command. 
```bash
go run <your file name ended with .go>
```
4. You will see the output `Hello COMP423` in your terminal. 

Alternatively, you can also use `build subcommand`. 
```bash
go build -o <your filename without .go>
```
It creates an executable binary file without running it. 
```bash
./<your filename without .go>
```
You will see the output `Hello COMP423` in your terminal. 

!!! Difference between build and run

    `go run` combines compilation and execution into one step whereas `go build` only complies the program into a binary file and requires an additional step to run the binary file. `go build` is similar to `gcc` in the way that it complies the source code into an executable binary format. 
    
5. You have successfully run your first Go Program. 

## Push Your Changes
Run the following command. 
```bash
git add .
git commit -m <your commit message
git push origin main
```
If being run successfully, you can see your Go program file in your Github repository. 