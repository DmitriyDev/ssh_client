# SSH client


Supports password connection.

Certificate connection doesn't checked yet.

***

Basic usage:


    func getDefaultConnectionConfig() *SSHClient {
        return &SSHClient{
            Ip:   "[host]",
            User: "[user]",
            Port: 22,
            Cert: "[password]",
        }
    }
    
    func main() {
        reader := bufio.NewReader(os.Stdin)
        connection := getDefaultConnectionConfig().Connect(CERT_PASSWORD)
        defer connection.Close()
        
        for {
            fmt.Print("$ ")
            cmdString, err := reader.ReadString('\n')
            if err != nil {
                fmt.Fprintln(os.Stderr, err)
            }
            err, out := connection.RunCmd(cmdString)
            if err != nil {
                fmt.Fprintln(os.Stderr, err)
            }
            fmt.Fprintln(os.Stdout, out)
        }
    
    }
