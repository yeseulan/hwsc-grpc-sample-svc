
# hwsc-grpc-sample

Sample HWSC service using gRPC in GoLang

### Creating HWSC GoLang Service

1. Install go version [go 1.11.1](https://golang.org/dl/)
2. Configure terminal $GOPATH, $GOROOT, and add your go workspace bin in $PATH in your ~/.bash_profile (**your paths may vary**)

   ```bash
   # this is my sample ~/.bash_profile
   PATH="/Library/Frameworks/Python.framework/Versions/3.7/bin:${PATH}"
   export PATH
   export GOROOT="/usr/local/go"
   export GOPATH="$HOME/go_workspace"
   export PATH="$HOME/protobuf-3.6.1/src:$HOME/go_workspace/bin:$PATH"

   parse_git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
   }
   
	export PS1="\[\033[36m\]\u\[\033[32m\]:\[\033[33;1m\]\w\[\033[32m\]\$(parse_git_branch)\[\033[m\]\$ "
	export CLICOLOR=1
	export LSCOLORS=ExFxBxDxCxegedabagacad
	alias ls='ls -GFh'
   ```
3. Run ``$ go get -u github.com/golang/dep/cmd/dep`` (GoLang Dependency Management)
4. Run ``$ bash $GOPATH/src/github.com/golang/dep/cmd/dep/install.sh``
5. Verify dep installation ``$ dep version``
6. Make a new GitHub repository. (Assuming we are creating a new service repo https://github.com/faraonc/empty-sample)
7. Run ``$ go get -u github.com/faraonc/empty-sample``
8. Change Directory ``$ cd $GOPATH/src/github.com/faraonc/empty-sample``
9. Run the following commands
   ```bash
   $ dep init
   $ ls
     Gopkg.toml Gopkg.lock vendor/
   ```
10. Make main.go file
       ```go
        package main
    
        import (
        	"fmt"
        )
        
        func main() {
        	fmt.Println("Hello, playground")
        }
    
       ```
11. Add gRPC dependency, ``$ dep ensure -add google.golang.org/grpc``
12. Modify Gopkg.toml to point to a gRPC specific commit revision
      ```toml
      [[constraint]]
      name = "google.golang.org/grpc"
      revision ="8dea3dc473e90c8179e519d91302d0597c0ca1d1"
      ```
11. Download and extract [protocol buffers 3.6.1](https://github.com/protocolbuffers/protobuf/releases)
12. Add the protoc binary to your $PATH (refer to step 2)
13. Define your proto; [basic guide](https://grpc.io/docs/tutorials/basic/go.html), [REST guide](https://grpc.io/blog/coreos), [example](https://github.com/faraonc/hwsc-grpc-sample/tree/master/proto)
14. Make a generate protoc script, [example](https://github.com/faraonc/hwsc-grpc-sample/blob/master/generate_proto.sh)
15. Run ``$ dep ensure -v`` from the root folder of the project to populate dependencies in the vendor folder (run as you add external dependencies)
16. Run your generate protoc script or as needed, [example result](https://github.com/faraonc/hwsc-grpc-sample/blob/master/proto/grpc-sample.pb.go)
17. TODO Defining a server