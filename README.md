# bu_rcs.coldfront

To intialize a new instance deployed using this collection:

Intialize database:

```
podman exec <app> coldfront initial_setup --force_overwrite
```

Collect static files:

```
podman exec <app> coldfront collectstatic --noinput
```

Creat an admin account:

```
podman exec <app> coldfront shell --no-imports -c "
from django.contrib.auth.models import User
u, created = User.objects.get_or_create(
    username='<username>',
    defaults={'email': '<email@bu.edu>', 'first_name': '<fn>',
              'last_name': '<ln>', 'is_active': True})
u.is_superuser = True
u.is_staff = True
u.set_unusable_password()
u.save()
print('created' if created else 'updated', u.username, u.is_superuser, u.is_staff)
"
```
