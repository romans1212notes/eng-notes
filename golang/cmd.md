# golang cmd
## Run command
```go
func runCommand(t *testing.T, command string, args []string) {
        cmd := exec.Command(command, args...)
        out, err := cmd.CombinedOutput()
        if err != nil && testing.Verbose() {
                fmt.Println("command:", command, args, ", output:", string(out))
        }
        assert.NoError(t, err)
}
```

## Set working directory
https://stackoverflow.com/questions/43135919/how-to-run-a-shell-command-in-a-specific-folder-with-golang
```go
cmd:= exec.Command("git", "log")
cmd.Dir = "your/intended/working/directory"
out, err := cmd.Output()
```
Seems that it is still using chdir internally, but doesn't affect the Golang process's current working dir.

## Bash and wildcard
https://stackoverflow.com/questions/10781516/how-to-pipe-several-commands-in-go
```
func getCPUmodel() string {
        cmd := "cat /proc/cpuinfo | egrep '^model name' | uniq | awk '{print substr($0, index($0,$4))}'"
        out, err := exec.Command("bash","-c",cmd).Output()
        if err != nil {
                return fmt.Sprintf("Failed to execute command: %s", cmd)
        }
        return string(out)
}
```
Tricky part is, this doesn't work
```
cmd := "'cat *.*'" // doesn't work
```
Also, this command will fail if there is sub-directory
```
cmd := "cat *" // doesn't work because it tries to cat sub directory and it will fail
```

## Run with timeout
* search "golang cmd exec timeout"
* https://stackoverflow.com/questions/11886531/terminating-a-process-started-with-os-exec-in-golang
* https://gist.github.com/scottcagno/7f7f372429c03b2fd404726084eacf3e
* https://medium.com/@vCabbage/go-timeout-commands-with-os-exec-commandcontext-ba0c861ed738
* https://github.com/golang/go/issues/9580

## Kill a process
* how to kill its subprocesses
* signal
  * https://github.com/golang/go/issues/7938
  * ProcessState and WaitStatus: https://github.com/golang/go/issues/19798

