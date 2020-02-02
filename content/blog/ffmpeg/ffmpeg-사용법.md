---
title: ffmpeg 사용법
date: 2020-02-02 20:02:63
category: ffmpeg
draft: false
---

![ffmpeg image](./images/ffmpeg_image.jpeg)

## 동영상 자막 입히기

### ASS 자막으로 변환하기

```bash
ffmpeg -i movie.srt movie.ass
//ass 자막은 Fontname, Fontsize 변경 가능하다
```

### 자막 입히기

```bash
    ffmpeg -i movie.mkv -vf subtitles=subtitle.ass out.mkv
﻿
    ffmpeg -i movie.mkv -vf "ass=sustitle.ass" out.mkv
﻿
    ffmpeg -i movie.mkv -vf subtitles=movie.mkv out.mkv
    // 동영상이 자막을 포함하는 경우
﻿
    ffmpeg -i movie.mkv -vf subtitles=movie.mkv:si=1 out.mkv
    // 이 명령어는 mkv 동영상에서 두번째 자막을 선택하라는 뜻
```

### 자막 추출

```bash
ffmpeg -i movie.mkv out.srt
// 간단히 out.srt 라고 지정해도 자막이 추출된다.
﻿
ffmpeg -i movie.mkv -map 0:15 out.srt
// 자막이 여러개 있을 경우 map 명령어로 STREAM을 지정할 수 있다.
﻿
```

## 동영상 변환

### 동영상 코덱 관리

```bash
ffmpeg -i movie.mkv -vcodec h264 -acodec aac out.mkv
// 비디오 코덱은 h264, 오디오 코덱은 aac 를 지정한 경우
﻿
ffmpeg -i sample.mkv -c:v h264 -c:a aac out.mkv
// 비디오 코덱은 h265, 오디오 코덱은 aac 를 지정한 경우
﻿
ffmpeg -i sample.mkv -c:v copy -c:a aac out.mkv
// 비디오 코덱은 copy(기존꺼 그대로), 오디오 코덱은 aac 를 지정한 경우
// 인코딩 속도가 빨라짐.
﻿
```
