---
layout: post
title:  PDF 문서에 이미지 삽입하기
date:   2018-05-29 01:00:00 +0300
description: # Add post description (optional)
img:  2018-05-29.jpg # Add image post (optional)
tags: [python, reportlab, pypdf2, image, pdf]
author:  # Add name author (optional)
---
# Intro
pdf 문서에 도장 및 워터마크 와 같은 이미지를 삽입할 수 있는 python 예제입니다.
<br>
<br>
<br>
<br>

# 패키지 설치
```
> pip install reportlab
> pip install pypdf2
```
<br>
<br>
<br>

# 예제
{% highlight Python %}
import os
from PyPDF2 import PdfFileReader, PdfFileWriter
from reportlab.pdfgen import canvas


# 1. 이미지가 삽입 될 빈 pdf 문서를 만든다.
c = canvas.Canvas('stamp.pdf')

# 2-1. 이미지의 검은색을 투명처리 (자세한 설명은 문서 하단에 정리)
mask = [0, 0, 0, 0, 0, 0]
# 2-2. 생성한 빈 pdf 문서에 이미지를 삽입(draw)한다. (좌표참고: 좌측하단이 0, 0)
c.drawImage('heum_stamp.png', x=500, y=50, width=44, height=44, mask=mask)
c.save()

# 3. 방금 생성한 pdf 문서를 연다.
stamp = PdfFileReader(open('stamp.pdf', 'rb'))

# 4. 출력을 위한 객체 생성
output_file = PdfFileWriter()

# 5. 이미지가 들어갈 원본 pdf 문서를 연다.
input_file = PdfFileReader(open('원천징수영수증.pdf', 'rb'))

# 6. 원본 pdf 문서의 전체 페이지 값을 가져온다.(총 3페이지이면 3이 출력)
page_cnt = input_file.getNumPages()

# 7. 이미지가 삽입 될 페이지 리스트 setting
insert_page = [1, 3]

# 8. 이미지가 삽입된 빈 문서와 원본 문서를 페이지별로 merge
for page_num in range(page_cnt):
    input_page = input_file.getPage(page_num)
    if page_num in [num-1 for num in insert_page]:
        print('insert image page {} of {}'.format(page_num+1, page_cnt))
        input_page.mergePage(stamp.getPage(0))
    output_file.addPage(input_page)

# 9. 'out_file'을 pdf 문서로 출력
with open('output_원천징수영수증.pdf', 'wb') as outputStream:
    output_file.write(outputStream)
{% endhighlight %}
<br>
<br>
<br>

# drawImage()의 'mask' 파라미터 설명
```
'mask' 파라미터는 투명한 색상을 설정할 때 사용됩니다.
6 개 숫자로 이루어진 list가 필요합니다.
6개의 숫자는 RGB 값의 범위를 의미하며, 해당 범위안에 있는 색상은 투명하게 처리됩니다.
예를 들어 [0,2,40,42,136,139]를 사용하면
0~2는 Red의 범위, 40~42은 Green, 136~139는 Blue 범위의 픽셀을 마스크합니다.
참고로 rgb는 0-255 사이의 값으로 이루어져 있습니다.
```
<br>
<br>
<br>

> reference

> [https://stackoverflow.com/questions/2925484/place-image-over-pdf][reference1]

[reference1]: https://stackoverflow.com/questions/2925484/place-image-over-pdf
