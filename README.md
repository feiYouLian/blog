## 项目搭建

```shell
# 创建mod
go mod init go mod init github.com/feiYouLian/blog

# 加载 依赖
go get -u github.com/spf13/cobra/cobra

# 初始化项目
cobra init --pkg-name github.com/feiYouLian/blog -a feiyl -l mit

# clean 依赖
go mod tidy

# 获取help go run .\main.go blog -h
go run .\main.go blog --help

# 编译
go build  -o blog .

# 编译后测试
blog --help

# 创建子命令 new
cobra add  new

# 执行 new
go run .\main.go new
```

## update new.go

```diff
+var foo *string
```

```go
// newCmd represents the new command
var newCmd = &cobra.Command{
	Use:   "new",
	Short: "A brief description of your command",
	Long: `A longer description that spans multiple lines and likely contains examples
and usage of using your command. For example:

Cobra is a CLI library for Go that empowers applications.
This application is a tool to generate the needed files
to quickly create a Cobra application.`,
	Args: func(cmd *cobra.Command, args []string) error {
		if len(args) != 1 {
			return errors.New("requires a  argument")
		}
		return nil
	},
	Run: func(cmd *cobra.Command, args []string) {
		fmt.Println("new called")
```

```diff
+               fmt.Println(args)
+               fmt.Printf("%s %s \r\n", "flag foo=", *foo)
+               // 自定义开发 coding
```

```go

        },

}

func init() {
rootCmd.AddCommand(newCmd)

    // Here you will define your flags and configuration settings.
    // Cobra supports Persistent Flags which will work for this command
    // and all subcommands, e.g.:
```

```diff
-   // newCmd.PersistentFlags().String("foo", "",  "A help for foo usage")
```

```diff
+   foo = newCmd.PersistentFlags().StringP("foo", "f", "default value", "A help for foo usage")
```

```go




    // Cobra supports local flags which will only run when this command
    // is called directly, e.g.:
    // newCmd.Flags().BoolP("toggle", "t", false, "Help message for toggle")

}

```

## cobra 代码的套路

```shell
# exe       go
# command   get
# flag      -u
# args      test.com/a/b
go get -u test.com/a/b

# exe       go run .\main.go
# command   new
# flag
# args      xxx
go run .\main.go  new xxx


# exe       go run .\main.go
# command   new
# flag      -f=fff
# args      xxx
go run .\main.go  new -f fff xxx
go run .\main.go  new -f=fff xxx
go run .\main.go  new  xxx -f=fff

# exe       blog
# command   new
# flag
# args      xxx
blog new xxx


```

```

```

```

```

```

```
