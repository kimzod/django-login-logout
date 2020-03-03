## 장고로 구현하는 로그인, 로그아웃
<br><br>

**setting.py**
    
    # redirect 를 블로그 메인으로 설정
    LOGIN_REDIRECT_URL = '/'


<br><br>
**url.py**

    from django.contrib.auth import views as auth_views
    
    # 클래스뷰 형식으로 설정
    path('login/', auth_views.LoginView.as_view(template_name='users/login.html'), name='login'),
    path('logout/', auth_views.LogoutView.as_view(template_name='users/logout.html'), name='logout'),
    
    
<br><br>
**login.html**
    
    {% extends "blog/base.html" %}
    {% load crispy_forms_tags %}
    {% block content %}
     # 회원가입 폼을 활용
        <div class="content-section">
            <form method="post">
                {% csrf_token %}
                <fieldset class="form-group">
                    <legend class="border-bottom mb-4">로그인</legend>
                    {{ form|crispy }}
                </fieldset>
                <div class="form-group">
                    <button class="btn btn-outline-info" type="submit">로그인</button>
                </div>
            </form>
            <div class="border-top pt-3">
                <small class="text-muted">계정이 없으신가요? <a href="{% url 'register' %}" class="ml-2">회원가입</a></small>
            </div>
        </div>
    {% endblock content %}
    
    
<br><br>
**logout.html**    

    {% extends "blog/base.html" %}
    {% block content %}
        <h2>로그아웃 되었습니다.</h2>
        <div class="border-top pt-3">
            <small class="text-muted">다시 로그인을 원하시면 <a href="{% url 'login' %}" class="ml-2">로그인</a></small>
        </div>
    {% endblock content %}
    
    
<br><br>
**base.html**      

    {% if user.is_authenticated %}
        <a href="{% url 'logout' %}" class="nav-item nav-link">로그아웃</a>
    {% else %}
        <a href="{% url 'login' %}" class="nav-item nav-link">로그인</a>
        <a href="{% url 'register' %}" class="nav-item nav-link">등록</a>
    {% endif %}
    
    
<br><br>    
    
    
    
