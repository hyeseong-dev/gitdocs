# Validator 패키지

## 특정 확장자만 파일 업로드 가능하게 만들기 \(pdf\)

백엔드에서 파일을 전달 받을때 특정 값의 파일만 전달 받게 유효성 검사를 통해서 내가 받고 싶은 파일만 업로드 가능하게 할 수 있다. 즉, 그런 작업을 위한 유효성 검사툴이 각 프레임 워크별로 존재한다.

역시나 장고는 vaildator가 역시 내장되어 있었다. 하지만 재대로 사용하는 방법을 정확하게 몰라서 찾아봤다.

**Django에서 model에서 validators를 사용하는 방식**

```text
from django.core.validators import FileExtensionValidator
from django.db import models 

class MyModel(models.Model):    
    pdf_file = models.FileField(upload_to='foo/',
                                validators=[FileExtensionValidator(allowed_extensions=['pdf'])])
```

간단하게 vaildator를 통해서 처리하는 방식이 가장 이상적 다른 방식은 아예 validator를 함수화하거나 모듈화해서 그걸 끌어와서 해결하는 방식입니다.

링크에서도 확인했지만 위의 **코드는 안전하지 않다는 것**이 문젠데  
효성 검사를 하면 실제로 파일 뒤의 글자 .pdf만되면 통과가 되기 때문.

그래도 프론트쪽에서 유효성 검사를 통해서 처리하는 방식을 하는 것과 병행하여 사용하는 것도 나쁘진 않아보입니다.

[https://stackoverflow.com/questions/3648421/only-accept-a-certain-file-type-in-filefield-server-side](https://stackoverflow.com/questions/3648421/only-accept-a-certain-file-type-in-filefield-server-side)  


