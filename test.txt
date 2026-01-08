// vuln.c - 测试案例
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {
    char buf[100];
    ssize_t len = read(0, buf, sizeof(buf) - 1);
    if (len <= 0) return 0;
    buf[len] = '\0';
    
    if (buf[0] == 'F') {              // 分支1：覆盖边+2
        printf("Found F\n");
        if (buf[1] == 'U') {          // 分支2：覆盖边+2
            printf("Found U\n");
            if (buf[2] == 'Z') {      // 分支3：覆盖边+2
                printf("Found Z\n");
                if (buf[3] == 'Z') {  // 分支4：触发崩溃
                    printf("CRASH!\n");
                    abort();
                }
            }
        }
    }
    return 0;
}