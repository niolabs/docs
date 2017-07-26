# Additional APIs #

{{ book.product }} has some additional APIs that you may find useful as you explore what {{ book.product }} has to offer.

## Configuration Refresh API ##

The ``/config/refresh`` endpoint is used when you update block or service configuration files through some means outside of the {{ book.product }} ``blocks`` and ``services`` APIs. For example, if you use a text editor to modify a block configuration file, you will need to tell a running {{ book.product }} instance to use those changes:

    curl -XGET 'localhost:8181/config/refresh' --user 'Admin:Admin'
