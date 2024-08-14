``` Groovy
// 定义 创建打包任务  
tasks.register('taskName', Jar) {  
    // 依赖于build任务  
    dependsOn('build')  
  
    // 任务在哪个文件夹下  
    group = 'taskGroup'  
  
    // JAR 文件的基本名称  
    archiveBaseName.set('jar_name')  
    // 指定输出路径  
    destinationDirectory.set(file('output'))  
  
    manifest {  
        attributes(  
                // 设置主类  
                'Main-Class': 'com.example.Example'  
        )  
    }  
  
    // 设置重复文件策略 排除  
    duplicatesStrategy = DuplicatesStrategy.EXCLUDE  
  
    // 包含所有子模块和依赖  
    from {  
        configurations.runtimeClasspath.collect {  
            it.isDirectory() ? it : zipTree(it)  
        } + (sourceSets.main.output as Iterable<Object>)  
    }  
}
```