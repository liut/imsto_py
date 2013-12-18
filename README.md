
#imsto-go client in python

## installation

`sudo pip-2.7 install -e .` (recommend)
or
`sudo python setup.py install`

## django settings

`settings.py`:

~~~
DEFAULT_FILE_STORAGE = 'imsto_client.django.ImageStorage'
IMSTO_HOST = 'localhost:8964'
IMSTO_ROOF = 'demo'
IMSTO_URL_PREFIX = '/'
IMSTO_THUMB_PATH = '/thumb'
~~~

`admins`

~~~
from django.contrib import admin
from imsto_client.django.widgets import AdminImageWidget

class GoodsAdmin(admin.ModelAdmin):

	def formfield_for_dbfield(self, db_field, **kwargs):
		if db_field.name == 'image_path':
			request = kwargs.pop("request", None)
			kwargs['widget'] = AdminImageWidget
			return db_field.formfield(**kwargs)
		return super(GoodsAdmin,self).formfield_for_dbfield(db_field, **kwargs)

	"""more other methods""

~~~

## nginx configuration

see also: imsto-go/INSTALL.md
