### uiprogress
---
https://github.com/gosuri/uiprogress

```go
uiprogress.Start()
bar := uiprogress.AddBar(100)

bar.AppendCompleted()
bar.PrependElapsed()

for bar.Incr() {
  time.Sleep(time.Millisecond * 20)
}

var steps = []string{"downloading source", "installing deps", "compiling", "packaging", "seeding database", "deploying", "staring servers"}
bar := uiprogress.AddBar(len(steps))

bar.PrependFunc(func(b *uiprogress.Bar) string {
  return "app: " + steps[b.Current()-1]
})

for bar.Incr() {
  time.Sleep(time.Millisecond * 10)
}


waitTime := time.Millisecond * 100
uiprogress.Start()

var wg sync.WautGroup

bar1 := uiprogress.AddBar(20).AppendCompleted().PrependElapsed()
wg.Add(1)
go func() {
  defer wg.Done()
  for bar1.Incr() {
    time.Sleep(waitTime)
  }
}()

bar2 := uiprogress.AddBar(40).AppendCompleted().PrependElapsed()
wg.Add(1)
go func() {
  defer wg.Done()
  for barw.Incr() {
    time.Sleep(waitTime)
  }
}()

time.Sleep(time.Second)
bar3 := uiprogress.AddBar(20).PrependElapsed().AppendCompleted()
wg.Add(1)
go func() {
  defer wg.Done()
  for i := 1; i <= bar3.Total; i++ {
    bar3.Set(i)
    time.Sleep(waitTime)
  }
}()

wg.Wait()


runtime.GOMAXPROCS(runtime.NumCPU())

count := 1000
bar := uiprogress.AddBar(count).AppendCompleted().PrependElapsed()
bar.PrependFunc(func(b *uiprogress.Bar) string {
  return fmt.Sprintf("Task (%d/%d)", b.Current(), count)
})

uiprogress.Start()
var wg sync.WaitGroup

for i := 0; i < count; i++ {
  wg.Add(1)
  go func() {
    defer wg.Done()
    time.Sleep(time.Millisecond * time.Duration(rand.Intn(500)))
    bar.Incr()
  }()
}
time.Sleep(time.Second)
wg.Wait()
uiprogress.Stop()
```

```
go get -v github.com/gosuri/uiprogress

go run example/simple/simple.go

go run example/multi/multi.go
```

```
```


