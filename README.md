# 支持utf-8中文正常显示

# 示例
```go
func TestDeCompressZip(t *testing.T) {
	password := "password"
	file, err := os.Open("test.zip")
	if err != nil {
		log.Fatal(err)
		return
	}
	readAll, err := io.ReadAll(file)
	if err != nil {
		log.Fatal(err)
		return
	}
	err, files := DeCompressZip(readAll, password)
	if err != nil {
		log.Fatal(err)
		return
	}
	for _, file := range files {
		fmt.Printf("文件名: %s\n", file.Name)
	}
}

func TestWriterUTF8(t *testing.T) {
	create, _ := os.Create("test.zip")
	writer := NewWriter(create)
	defer writer.Close()

	encrypt, err := writer.Encrypt("哈哈哈.txt", "password")
	if err != nil {
		log.Fatal(err)
		return
	}

	_, err = io.Copy(encrypt, bytes.NewReader([]byte("hello 你好 !!")))
	if err != nil {
		log.Fatal(err)
		return
	}
	writer.Flush()
}

```