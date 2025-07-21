FROM golang:1.18 AS builder

WORKDIR /app

COPY main.go .

RUN go mod init guestbook
RUN go mod tidy

RUN go build -o main main.go

FROM ubuntu:18.04

# Copiamos el binario compilado desde la etapa de build
COPY --from=builder /app/main /app/guestbook

# Copiamos los archivos estáticos
COPY public/index.html /app/public/index.html
COPY public/script.js /app/public/script.js
COPY public/style.css /app/public/style.css
COPY public/jquery.min.js /app/public/jquery.min.js

WORKDIR /app

# Exponemos el puerto que usa la aplicación
EXPOSE 3000

# Comando por defecto al iniciar el contenedor
CMD ["./guestbook"]
