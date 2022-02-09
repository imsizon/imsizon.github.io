---
date: 2011-08-02 09:43:44
title: Shell脚本中加点scala的料
source: http://blog.getintheloop.eu/2011/08/01/system-scripting-with-scala/
categories: 
- 杂记
slug: System Scripting with Scala
---

在bash脚本中直接写scala并且和普通脚本一样运行：

```sca
#!scala
#!/bin/sh
SCRIPT="$(cd "${0%/*}" 2>/dev/null; echo "$PWD"/"${0##*/}")"
DIR=`dirname "${SCRIPT}"}`
exec scala $0 $DIR $SCRIPT
::!#

import java.io.File

object App {
  def main(args: Array[String]): Unit = {
    val Array(directory,script) = args.map(new File(_).getAbsolutePath)
    println("Executing '%s' in directory '%s'".format(script, directory))
  }
}
```

魔法之处在哪里呢？看原文作者的解释：

>Notice the base code between #!/bin/sh and ::!#. This allows you to execute bash script (or whatever script you want) before evaluating this file as a Scala script. This can be pretty handy for certain tasks when doing system scripting
