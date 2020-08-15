# Part 1 \| 앱 설정

## **Step 1 \| 장고 설치**

```text
pip install Django
```

## **Step 2 \| 프로젝트 시작**

```text
django-admin startproject ecommerce
cd ecommerce
```

## **Step 3 \| 앱 생성**

```text
python manage.py startapp store
```

## **Step 4 \| settings.py에 app등**

{% tabs %}
{% tab title="ecommerce/ecommerce/settings.py" %}
```text
INSTALLED_APPS = [
...,
...,
...,

'store',
]
```
{% endtab %}
{% endtabs %}



