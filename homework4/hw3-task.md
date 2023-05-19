Чернышева Анна 
ЦП | Разработчик. Программист (Frontend) | 3416 | 2

# Контейнеризация (семинары)

## Урок 4. Dockerfile и слои

Задание: необходимо создать Dockerfile, основанный на любом образе (вы в праве выбрать самостоятельно).
В него необходимо поместить приложение, написанное на любом известном вам языке программирования (Python, Java, C, С#, C++).

При запуске контейнера должно запускаться самостоятельно написанное приложение.

```
mkdir /home/slava/java_app
cd /home/slava/java_app
nano Main.java
```

```
import java.util.Scanner;


public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        System.out.print("Enter a number: ");
        int n = in.nextInt();
        for (int i = 1; i <= n; i++) {
            int count = 1;
            for(int j = 1; j <= i; j++) {
                for (int k = 1; k <= j; k++) {
                    if(count <=i) {
                        System.out.print(j);
                    }
                    if(count <i) {
                        System.out.print(" ");
                    }
                    count++;
                }
            }
            if ( i < n) {
                System.out.println();
            }
        }
    }
}
```

nano Dockerfile

FROM openjdk:20
RUN rm -rf /var/lib/apt/lists/*
COPY . /usr/src/myapp
WORKDIR /usr/src/myapp
RUN javac Main.java
CMD ["java", "Main"]
dockerbuild -t java .
docker run -it --rm java
```
