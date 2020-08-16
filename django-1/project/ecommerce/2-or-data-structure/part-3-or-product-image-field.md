# Part 3 \| Product Image Field

## 들어가기 앞서 

이제 이미지 필드를 모델에 추가해보도록 할게요.  
그리고 준비물로 이미지 몇장도 준비해 볼게요. 

헤드폰, 책, 소스코드, 시계, 신발, 티셔츠에 해당하는 이미지를 다운받아주세요.  
\(단, static/image/폴더에 두지 마세요.\)  


## Step 1 \| ImageField\(\)

### 1 - Add ImageField\(\)

Product model에서 image 변수를 만들게요. 

![](../../../../.gitbook/assets/image%20%28468%29.png)

### 2 - pip install Pillow

이대로 python manage.py makemigration과 migrate를 하면 오류 메시지가 나올텐데요.   
자세히보면 Pillow라는 라이브러리 설치를 요청할거에요. 

```text
$ pip install Pillow
```

#### Pillow는 기본적으로 파이썬 이미지 라이브러리에요. 

{% embed url="https://pillow.readthedocs.io/en/stable/" %}

### 3 - Run Migrations

이제 아까 하다가 오류 났던 makemigrations 과 migrate 명령어를 CLI에서 실행해주세요.



## Step 2 \| Media\_Root

업로드한 이미지가 어디에 저장될지 설정을 해줘야하는데요. settings.py파일 안을 보면   
화살표가 가리키는 MEDIA\_ROOT 변수가 있는데요. 저렇게 작성해주세요.

![](../../../../.gitbook/assets/image%20%28474%29.png)

이제는 관리자 화면에서 각각의 상품의 Image를 업로드 할 수 있게 되었어요.  
6가지 품목 모두다 제품에 해당하는 이미지를 업로드하고 저장하도록 할게요. 

![](../../../../.gitbook/assets/image%20%28430%29.png)



## Step 3 \| Media\_URL

그런데 해당 제품의 사진 URL로 가보면 여전히 오류가 뜨는데요. URL 설정이 필요하다고 하네요.

![](../../../../.gitbook/assets/image%20%28458%29.png)



![](../../../../.gitbook/assets/image%20%28427%29.png)

이전에 MEDIA\_ROOT 바로 위에 MEDIA\_URL을 작성하도록 할게요.  
이 역활은 media root가 항상 'images/image\_name'으로 시작되도록 url 이름을 설정해주는거에요. 

## Step 4 \| urls.py configurations

### 1 - Imports

root urls.py파일에서 필요한 패키지 or 파일, 메소드를 import할게요. 

![](../../../../.gitbook/assets/image%20%28443%29.png)

### 2 - Add URL Path

![](../../../../.gitbook/assets/image%20%28446%29.png)

![](../../../../.gitbook/assets/image%20%28421%29.png)

urls.py까지 설정을 마치면 해당 이미지의 url이 각각 잘 설정 되게 나타납니다.

## Step 5 \| Render Images

이번에는 이미지 랜더링을 해볼게요. 

```text
<img class="thumbnail" src="{% product.image.url %}"
```

그런데 만약 관리자 페이지에서 등록된 상품의 이미지중 하나를 지우면 페이지 오류가 발생해요.   
이를 해결해 볼게요. 

## Step 6 \| Image Error Solution

Product 모델안에 imageURL 메서드를 만들게요. 그리고 머리에는 property 데코레이터를 둬서 메서드를 메서드로 활용한다기보다 attribute\(속성\)성질을 가지게 만들어요.   
  
즉, 이렇게 오류가 빈번하게 날 수 있는 부분의 경우 try except구문을 통해서 서버를 다운시키지 않고 돌릴수 있게 되요.

```text
class Product(models.Model):
	...
	...
	...
	image = models.ImageField(null=True, blank=True)

	def __str__(self):
		return self.name

	@property
	def imageURL(self):
		try:
			url = self.image.url
		except:
			url = ''
		return url
```

