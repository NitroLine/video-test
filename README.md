# video-test

Необходимо сделать API для сервиса хранения видеофайлов с возможностью менять разрешениe. Ковертация должа проиcходит с помощью **ffmpeg** (либо обертки над ffmpeg)


## HTTP API

### Методы

#### `POST /file/`
Тело запроса: видеофайл в формате MP4.

В теле ответа возвращается 
```
{
  id: UUID — идентификатор , например: `876b8335-3279-4f59-9718-570f37f076ea`.
}
``` 

Код ответа: `200 Ok`.

#### `PATCH /file/{id}/`
Начать изменение разрешения видео используя ffmpemg. Ответ должен возвращться не зависимо от завершения процесса обработки (обработка не должена блокировать запрос) 

Тело запроса:

```
{
  width: int,
  height: int,
}
```

В теле ответа возвращается 
```
{
  success: Boolean
}
``` 
Код ответа: `200 Ok`.

#### `GET /file/{id}/`
Полуить информацию о файле и процессе его конвертации

Тело ответа:

```
{
  id: uid,
  filename: string,
  processing: Boolean - 
  processingSuccess: null | true | false  - отображет успешность последней опреции над видео. Дефолтное значение null.
}
```
Код ответа: `200 Ok`.


#### `DELETE /file/{id}/`
Удалить файл

В теле ответа возвращается 
```
{
  success: Boolean
}
``` 
Код ответа: `200 Ok`.


### Обработка ошибок
При возникновении ошибок необходимо возвращать ошибку в json формате
```
{
  error: string
}
```

## Дополнительно
Будет плюсом если:
 - есть автодокументация API 
 - есть система логирования
 - сервис завёрнут в docker контейнер
 - наличие юнит тестов

