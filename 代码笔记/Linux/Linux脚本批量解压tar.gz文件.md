
``` shell
# 解压到当前文件夹
ls *.tar.gz|xargs -n1 tar zxvf

# 解压到与文件同名的文件夹
for file in *.tar.gz; do mkdir -p "${file%%.*}" && tar -xf "$file" -C "${file%%.*}"; done
```