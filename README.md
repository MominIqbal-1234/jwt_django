# jwt_django

jwt_django is very useful package for django developers to create, read, authenticate jwt token. <br> jwt_django provide end-to-end control jwt token

# How to install jwt_django

```python
pip install jwt_django
```

# How to use jwt_django
### Configuration
```python
# setting.py
 INSTALLED_APPS = [
            ....
       'jwt_django',
       
        ]
```


```python
# views.py

from jwt_django.core import GenerateKey,JWTToken
from django.contrib.auth import authenticate




secret_key = GenerateKey.generate_key() # Create Every time new secret key, dont use production, in production use static key
user = JWTToken(secret_key=secret_key,expiry_token=5)



@api_view(['POST'])
def login(request):
    if request.method == 'POST':
        username = request.data["username"]
        password = request.data["password"]
        user_auth = authenticate(username=username, password=password)
     
        if user_auth is not None:
            token = user.createToken({
            "user_id":user_auth.id,
            "username":username
             })
            return Response({"token":token})
        return Response({"invalid-credentials":"Wrong username and password"})

```

### Pass Authorization Token

![Screenshot (78)](https://user-images.githubusercontent.com/61788052/219456256-9b0b2382-1ba6-4b96-8452-3ae21b449434.png)

````python


@api_view(['POST'])
def data_view(request):
    # Set header
    # Authorization:mytoken
    print(user.authuser(request,"user_id","username"))
    
   
    return Response({
       "username":user.authuser(request,"user_id","username")
    })

````

### Authenticated
````python

print(user.isAuthenticated(request)) # Return Bool
print(user.is_authenticated()) # Return Bool
````


### Pass Cache-Control Token


![Screenshot (80)](https://user-images.githubusercontent.com/61788052/219882873-ba1b846e-9d03-4404-a414-25ed36d03b7b.png)



````python
@api_view(['POST'])
def data_view(request):
    # Set header
    # Cache-Control:mytoken
    print(user.tokenInfo(request,"myinfo1","myinfo2"))
    
   
    return Response({
       "username":user.tokenInfo(request,"myinfo1","myinfo2")
    })
````


Check Our Site : https://mefiz.com </br>
Developed by : Momin Iqbal