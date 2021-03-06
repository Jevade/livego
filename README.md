<p align='center'>
    <img src='./logo.png' width='200px' height='80px'/>
</p>

[中文](./README_cn.md)

[![Test](https://github.com/gwuhaolin/livego/workflows/Test/badge.svg)](https://github.com/gwuhaolin/livego/actions?query=workflow%3ATest)
[![Release](https://github.com/gwuhaolin/livego/workflows/Release/badge.svg)](https://github.com/gwuhaolin/livego/actions?query=workflow%3ARelease)

Simple and efficient live broadcast server:
- Very simple to install and use;
- Pure Golang, high performance, cross-platform;
- Support commonly used transmission protocols, file formats, encoding formats;

#### Supported transport protocols
- RTMP
- AMF
- HLS
- HTTP-FLV

#### Supported container formats
- FLV
- TS

#### Supported encoding formats
- H264
- AAC
- MP3

## Installation
After directly downloading the compiled [binary file](https://github.com/gwuhaolin/livego/releases), execute it on the command line.

#### Boot from Docker
Run `docker run -p 1935:1935 -p 7001:7001 -p 7002:7002 -p 8090:8090 -d gwuhaolin/livego` to start

#### Compile from source
1. Download the source code `git clone https://github.com/gwuhaolin/livego.git`
2. Go to the livego directory and execute `go build` or `make build`

## Use
1. Start the service: execute the livego binary file or `make run` to start the livego service;
2. Get a channelkey from `http://localhost:8090/control/get?room={roomname}` and copy data like your channelkey.
3. Upstream push: Push the video stream to `rtmp://localhost:1935/{appname}/{channelkey}` through the` RTMP` protocol(default appname is `live`), for example, use `ffmpeg -re -i demo.flv -c copy -f flv rtmp://localhost:1935/{appname}/{channelkey}` push;
4. Downstream playback: The following three playback protocols are supported, and the playback address is as follows:
    - `RTMP`:`rtmp://localhost:1935/{appname}/{roomname}`
    - `FLV`:`http://127.0.0.1:7001/{appname}/{roomname}.flv`
    - `HLS`:`http://127.0.0.1:7002/{appname}/{roomname}.m3u8`
   
all options: 
```bash
./livego  -h
Usage of ./livego:
      --api_addr string       HTTP manage interface server listen address (default ":8090")
      --config_file string    configure filename (default "livego.yaml")
      --flv_dir string        output flv file at flvDir/APP/KEY_TIME.flv (default "tmp")
      --gop_num int           gop num (default 1)
      --hls_addr string       HLS server listen address (default ":7002")
      --httpflv_addr string   HTTP-FLV server listen address (default ":7001")
      --level string          Log level (default "info")
      --read_timeout int      read time out (default 10)
      --rtmp_addr string      RTMP server listen address (default ":1935")
      --write_timeout int     write time out (default 10)
```

### [Use with flv.js](https://github.com/gwuhaolin/blog/issues/3)

Interested in Golang? Please see [Golang Chinese Learning Materials Summary](http://go.wuhaolin.cn/)
