FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build-env
WORKDIR /app

COPY Common/Common.csproj ./Common/
COPY MultipleProject/MultipleProject.csproj ./MultipleProject/

RUN dotnet restore MultipleProject

COPY ./Common ./Common/
COPY ./MultipleProject ./MultipleProject/

RUN dotnet publish MultipleProject -c Release -o out

FROM mcr.microsoft.com/dotnet/aspnet:5.0
WORKDIR /app
COPY --from=build-env /app/out .

ENTRYPOINT [ "dotnet", "MultipleProject.dll" ]
