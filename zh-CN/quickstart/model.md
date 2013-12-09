# model分析
我们知道Web应用中我们用的最多的就是数据库操作，而model层一般用来做这些操作，我们的`bee new`例子不存在Model的演示，但是`bee api`应用中存在model的应用，说的简单一点，如果你的应用足够简单，那么Controller可以处理一切的逻辑，如果你的逻辑里面存在着可以复用的东西，那么就抽取出来变成一个模块，那么Model就是逐步抽象的过程，一般我们会在Model里面处理一些数据读取，如下是我日子分析应用中的代码片段：

```
package models

import (
	"loggo/utils"
	"path/filepath"
	"strconv"
	"strings"
)

var (
	NotPV []string = []string{"css", "js", "class", "gif", "jpg", "jpeg", "png", "bmp", "ico", "rss", "xml", "swf"}
)

const big = 0xFFFFFF

func LogPV(urls string) bool {
	ext := filepath.Ext(urls)
	if ext == "" {
		return true
	}
	for _, v := range NotPV {
		if v == strings.ToLower(ext) {
			return false
		}
	}
	return true
}
```

所以如果你的应用足够简单，那么就不需要Model了，如果你的模块开始多了，需要复用，需要逻辑分离了，那么Model是必不可少的。接下来我们将分析如何编写View层的东西。