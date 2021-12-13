# prometheus-2

We change the body of ```func TolerantVerifyLeak(m *testing.M)``` in file util/testutil/testing.go 
by applying the following patch. 

```go
func TolerantVerifyLeak(m *testing.M) {
-	goleak.VerifyTestMain(m,
-		// https://github.com/census-instrumentation/opencensus-go/blob/d7677d6af5953e0506ac4c08f349c62b917a443a/stats/view/worker.go#L34
-		goleak.IgnoreTopFunction("go.opencensus.io/stats/view.(*worker).start"),
-		// https://github.com/kubernetes/klog/blob/c85d02d1c76a9ebafa81eb6d35c980734f2c4727/klog.go#L417
-		goleak.IgnoreTopFunction("k8s.io/klog/v2.(*loggingT).flushDaemon"),
-	)
+	m.Run()
}

```
