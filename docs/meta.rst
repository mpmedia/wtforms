class Meta
==========

.. module:: wtforms.meta

the `class Meta` paradigm allows WTForms features to be customized, and even
new behaviors to be introduced. It also supplies a place where configuration
for any complementary modules can be done.

Typical usage looks something like::

    class MyForm(Form):
        class Meta:
            csrf = True
            locales = ('en_US', 'en')

        name = TextField(...)
        # and so on...

For the majority of users, using a class Meta is mostly going to be done for
customizing options used by the default behaviors, however for completeness
the entire API of the `Meta` interface is shown here.

.. autoclass:: DefaultMeta
    
    **Configuration**
    
    .. autoattribute:: csrf

        Setting ``csrf`` to `True` will enable CSRF for the form. The value can 
        also be overridden per-instance via instantiation-time customization
        (for example, if csrf needs to be turned off only in a special case)

        .. code-block:: python

            form = MyForm(request.form, meta={'csrf': False})

    .. autoattribute:: csrf_class

        If set, this is a class which is used to implement CSRF protection.
        Read the documentation on CSRF to get more information on how to use.

    .. autoattribute:: csrf_field_name

        The name of the automatically added CSRF token field.

    .. autoattribute:: locales

        Setting to a sequence of strings specifies the priority order
        of locales to try to find translations for built-in messages of 
        WTForms. If the value `False`, then strings are not translated 
        (the translations provider is a dummy provider)

    .. autoattribute:: cache_translations

        If `True` (the default) then cache translation objects. The default 
        cache is done at class-level so it's shared with all class Meta.

    **Advanced Customization**

    Usually, you do not need to override these methods, as they provide core
    behaviors of WTForms.

    .. automethod:: build_csrf

    .. automethod:: get_translations

    .. automethod:: bind_field

    .. automethod:: wrap_formdata

    .. automethod:: render_field
