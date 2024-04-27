# HttpComponent in maXbox5.1
Delphi component wrapper for WinInet library. Written in Delphi 2010.

![Screenshot 2024-04-25 210042](https://github.com/maxkleiner/HttpComponent/assets/3393121/00c84fc0-2f5a-457d-8d87-a86729c19765)

## How to use multipart with an real API

```
const URL_APILAY_DETECT = 'https://api.api-ninjas.com/v1/objectdetection/';

function TestHTTPClassComponentAPIDetection2(AURL, askstream, aApikey: string): string;
var HttpReq1: THttpRequestC;
    Body: TMultipartFormBody;
    Body2: TUrlEncodedFormBody;
begin
  Body:= TMultipartFormBody.Create;
  Body.ReleaseAfterSend:= True;
  //Body.Add('code','2','application/octet-stream');
  Body.AddFromFile('image', exepath+'randimage01.jpg');
  HttpReq1:= THttpRequestC.create(self);
  HttpReq1.headers.add('X-Api-Key:'+AAPIKEY);
  HttpReq1.headers.add('Accept:application/json');
  try
    if HttpReq1.Post1Multipart(AURL, body) then
       writeln(HttpReq1.Response.ContentAsString)
    else Writeln('APIError '+inttostr(HttpReq1.Response.StatusCode2));
  finally 
    writeln('Status3: '+gethttpcod(HttpReq1.Response.statuscode2))
    HttpReq1.Free;  
    sleep(200)
    // if assigned(body) then body.free;
  end; 
end;

println(TestHTTPClassComponentAPIDetection2(URL_APILAY_DETECT,' askstream',N_APIKEY));
 
```


## How to use

### GET
```
procedure TForm1.Button1Click(Sender: TObject);
begin
  if HttpRequest1.Get('https://httpbin.org/get') then
    ShowMessage(HttpRequest1.Response.ContentAsString)
  else
    ShowMessage('ERROR ' + getHttpcod(HttpRequest1.Response.StatusCode2));
end;
```
### POST
Posting a simple text:
```procedure TForm1.Button1Click(Sender: TObject);
begin
  if HttpRequest1.Post('https://httpbin.org/put', 'testing a POST') then
    ShowMessage(HttpRequest1.Response.ContentAsString)
  else
    ShowMessage('ERROR ' + IntToStr(HttpRequest1.Response.StatusCode2));
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

