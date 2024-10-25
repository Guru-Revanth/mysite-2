# mysite-2

## views.py

```
from django.http import HttpResponse, HttpResponseRedirect
from django.shortcuts import get_object_or_404, render
from django.urls import reverse
from django.views import generic
from django.utils import timezone

from .models import Choice, Question

class IndexView(generic.ListView):
    template_name = 'polls/index.html'
    context_object_name = 'latest_question_list'

    def get_queryset(self):
        """
        Return the last five published questions (not including those set to be
        published in the future).
        """
        return Question.objects.filter(
            pub_date__lte=timezone.now()
        ).order_by('-pub_date')[:5]


class DetailView(generic.DetailView):
    model = Question
    template_name = 'polls/detail.html'

    def get_queryset(self):
        """
        Excludes any questions that aren't published yet.
        """
        return Question.objects.filter(pub_date__lte=timezone.now())


class ResultsView(generic.DetailView):
    model = Question
    template_name = 'polls/results.html'


def vote(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    try:
        selected_choice = question.choice_set.get(pk=request.POST['choice'])
    except (KeyError, Choice.DoesNotExist):
        # Redisplay the question voting form.
        return render(request, 'polls/detail.html', {
            'question': question,
            'error_message': "You didn't select a choice.",
        })
    else:
        selected_choice.votes += 1
        selected_choice.save()
        # Always return an HttpResponseRedirect after successfully dealing
        # with POST data. This prevents data from being posted twice if a
        # user hits the Back button.
        return HttpResponseRedirect(reverse('polls:results', args=(question.id,)))


# New owner view function
def owner(request):
    return HttpResponse("Hello, world. c433ceb4 is the polls index.")
```

change views.py code also according to the before process

![image](https://github.com/user-attachments/assets/0e197298-8392-4960-89c9-b472b5586acb)

the last line of the code is 
```
"Hello, world. c433ceb4 is the polls index."
```
for me is that password only so i used c433ceb4 make you u have the same or different

or else change that line in your program

by help of this code

```
cd mysite-2
```

```
cd polls
```

```
vi views.py
```

```
press "I" for edit
```

go to bottom line and change password area

```
"Hello, world. <password> is the polls index."
```

you can view your password in below link

```
https://www.dj4e.com/tools/dj-tutorial/?PHPSESSID=4051f7108f01caec0382d203150859e9
```

after changing views.py press esc key and type

```
:wq
```

it will save automatically

now open urls.py with same process

```
vi urls.py
```

```
press "I" for edit
```

## urls.py

```
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('polls/', include('polls.urls')),
    path('admin/', admin.site.urls),
]
```

after changing urls.py press esc key and type

```
:wq
```

after editing urls.py and views.py now you should go to the old directory

```
cd ..
```

```
cd ..
```

if you give ls command in terminal you will be seeing mysite,polls,manage.py,readme.md,etc

```
python manage.py migrate
```

```
python manage.py collectstatic
```

