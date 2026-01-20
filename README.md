# Lab

EXPERIMENT 3
1.myapp/views.py 
from django.http import HttpResponse 
from datetime import datetime 
def current_datetime(request): 
    now = datetime.now() 
    html = f"<html><body>Current date and time: {now} </body></html>" 
    return HttpResponse(html)
2. myapp/urls.py
from django.urls import path 
from . import views 
urlpatterns = [ 
path('datetime/', views.current_datetime, 
name='current_datetime'), 
]
3. myproject/urls.py
from django.urls import include, path 
from myapp import views
urlpatterns = [ 
path('', views.current_datetime),
path('myapp/', include('myapp.urls')), 
] 

EXPERIMENT 4
1.myapp/views.py 
from django.http import HttpResponse 
from datetime import datetime, timedelta 
def offset_datetime(request): 
    now = datetime.now() 
    ahead = now + timedelta(hours=4) 
    before = now - timedelta(hours=4) 
    html = ( 
        f"<html><body>Current date and time: {now}<br>"
        f"4 hours ahead: {ahead}<br>" 
        f"4 hours before: {before}</body></html>" 
    ) 
    return HttpResponse(html)
2. myapp/urls.py
from django.urls import path 
from . import views 
urlpatterns = [ 
    path(
        'offset-datetime/', 
        views.offset_datetime, 
        name='offset_datetime'), 
] 
3. myproject/urls.py
from django.urls import include, path 
from myapp.views import offset_datetime
urlpatterns = [ 
    path('',offset_datetime),
    path('myapp/', include('myapp.urls')),  ]

    
EXPERIMENT 5
1.myapp/views.py 
from django.http import HttpResponse 

def display_lists(request): 
    fruits = ['Apple', 'Banana', 'Cherry', 'Date', 
              'Elderberry'] 
    students = ['Michael', 'Dwight', 'Jim', 'Pam', 
                'Kevin'] 
    html = """ 
    <html> 
    <body> 
    <h1>Unordered List of Fruits</h1> 
    <ul> 
    """ 
    for fruit in fruits: 
        html += f"<li>{fruit}</li>" 
    html += """ 
    </ul> 
    16 
    <h1>Ordered List of Selected Students</h1> 
    Full Stack Development – 21CD71 
    Lab Manual 
    <ol> 
    """ 
    for student in students: 
        html += f"<li>{student}</li>" 
    html += """ 
    </ol> 
    </body> 
    </html> 
    """ 
    return HttpResponse(html)
2. myapp/urls.py
from django.urls import path 
from . import views 

urlpatterns = [ 
    path('lists/', views.display_lists, name='display_lists'), 
]
3. myproject/urls.py
from django.urls import include, path 
from myapp.views import display_lists

urlpatterns = [ 
    path('',display_lists, name='home'),
    path('myapp/', include('myapp.urls')), 
]
