# Part 4 \| Static files

본격적인 템플릿 작업에 앞서서 정적파일\(static files\)혹은 images, css and js files들을 작업해볼게요. 

## **Step 1 \| "Static" Folder**

**프로젝트 폴더 안에 static 폴더를 만들어 주세요. 그리고 다시 그 폴더 안에 css, images 폴더를 만들게요.** 

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt4/1+static-folder.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt4/1+static-folder.png)

## **Step 2 \| CSS File**

**main.css 파일을 만들어 볼게요. 나중에 이 파일은 bootstrap CDN을 통해서 모든 페이지의 소스가 될 거에요.** 

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt4/2+body-color.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt4/2+body-color.png)



## **Step 3 \| STATICFILES\_DIRES**

**장고에게 static file의 위치를 알려줘야 해요.아래와 같 settings.py파일을 수정할게요.** 

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt4/3+static-settings.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt4/3+static-settings.png)

## **Step 4 \| Add Static Files to Page**

우선 store.html 페이지에 방금 것들을 적용해 볼게요.   
html의 link태그의 href속성 값을 jinja 문법을 이용했는데요. 이를 가능하게 연결 시켜준것이 

첫 번째줄의 {%load static %}입니다.

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt4/4+static-link.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt4/4+static-link.png)

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt4/5+background.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt4/5+background.png)

## **Step 5 \| Add Image**

아래 보이는 쇼핑카트 이미지를 입혀 보도록 할게요.

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt4/6+cart.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt4/6+cart.png)

  
[![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt4/7+static-image.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt4/7+static-image.png)

방식은 매우 비슷합니다. 

차이점은

1. link태그가 아닌 img태그
2. path가 기존과 다르다는거!

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt4/8+static-image-template.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt4/8+static-image-template.png)

