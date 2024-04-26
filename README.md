# HttpComponent in maXbox5.1
Delphi component wrapper for WinInet library. Written in Delphi 2010.

![Screenshot 2024-04-25 210042](https://github.com/maxkleiner/HttpComponent/assets/3393121/00c84fc0-2f5a-457d-8d87-a86729c19765)


## How to use

### GET
```
procedure TForm1.Button1Click(Sender: TObject);
begin
  if HttpRequest1.Get('https://httpbin.org/get') then
    ShowMessage(HttpRequest1.Response.ContentAsString)
  else
    ShowMessage('ERROR ' + IntToStr(HttpRequest1.Response.StatusCode));
end;
```
### POST
Posting a simple text:
```procedure TForm1.Button1Click(Sender: TObject);
begin
  if HttpRequest1.Post('https://httpbin.org/put', 'testing a POST') then
    ShowMessage(HttpRequest1.Response.ContentAsString)
  else
    ShowMessage('ERROR ' + IntToStr(HttpRequest1.Response.StatusCode));
end;
```
Posting a file with a Multipart form:
```
procedure TForm1.Button1Click(Sender: TObject);
var
  Body: TMultipartFormBody;
begin
  Body := TMultipartFormBody.Create;
  Body.ReleaseAfterSend := True;
  Body.Add('code', '2');
  Body.AddFromFile('image', 'C:\Users\User\Desktop\image.png');

  HttpRequest1.Post('https://httpbin.org/post', Body);
  ShowMessage(HttpRequest1.Response.ContentAsString);
end;
```
Posting a url encoded form:
```
procedure TForm1.Button1Click(Sender: TObject);
var
  Body: TUrlEncodedFormBody;
begin
  Body := TUrlEncodedFormBody.Create;
  Body.ReleaseAfterSend := True;
  Body.Add('code', '1');
  Body.Add('name', 'John');

  HttpRequest1.Post('https://httpbin.org/post', Body);
  ShowMessage(HttpRequest1.Response.ContentAsString);
end;
```

