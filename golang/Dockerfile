# Dockerfile for Go with vendor
FROM golang:1.22.5

WORKDIR /golang
# Copy go.mod and go.sum files to the workspace
COPY go.mod go.sum ./

# Copy the source from the current directory to the working directory inside the container
COPY . .

# Установите рабочий каталог, где находятся исходные файлы
WORKDIR /golang/apps/main

# Постройте Go приложение
RUN CGO_ENABLED=1 GOOS=linux go build -mod=vendor -a -installsuffix cgo -o main .


EXPOSE 9000

CMD ["./main"]
