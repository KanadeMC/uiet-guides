# Установка Swagger в проект
Создаём проект `Веб-API ASP.Net Core (Майкрософт)`
Но как мы можем видеть тут ни слова про **Swagger** поэтому сейчас будем это исправлять, для этого нам нужны 3 пакета NuGet:
- Swashbuckle.AspNetCore.Swagger
- Swashbuckle.AspNetCore.SwaggerUI
- Swashbuckle.AspNetCore.SwaggerGen
После чего можно приступать к изменению файла `Program.cs`:
```csharp
var builder = WebApplication.CreateBuilder(args);

// Add services to the container.

builder.Services.AddControllers();
// Learn more about configuring OpenAPI at https://aka.ms/aspnet/openapi
builder.Services.AddOpenApi(); // Эта строчка нам не нужна, убираем! 
builder.Services.AddSwaggerGen(); // Эту добавим чтобы подключить SwaggerGen в приложение

var app = builder.Build();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.MapOpenApi(); // Эта строчка нам не нужна, убираем
	app.UseSwagger(); // Подключаем Swagger
    app.UseSwaggerUI(); // Подключаем SwaggerUI
}

app.UseHttpsRedirection();

app.UseAuthorization();

app.MapControllers();

app.Run();
```
и теперь можем спокойно подключаться по адресу что первый выводится при запуске приложения в командной строке.
Так же не забудьте, если хотите открывать страницу не в браузере по умолчанию, выбрать ваш браузер в выпадающем списке справа от кнопки запуска проекта:
![Картинка 1](/image1.png)
Если все ещё не видите Swagger, даже после того как разрешили открывать небезопасную страницу (по мнению браузера), то попробуйте добавить к адресу /swagger, например
![Картинка 2](/image2.png)
Тут мы имеем адрес https://localhost:7240, если не получается зайти в интерфейс Swagger, по переходим по адресу https://localhost:7240/swagger
