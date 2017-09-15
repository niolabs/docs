# Additional APIs

{{ book.product }} has  additional APIs that you may find useful as you explore what {{ book.product }} has to offer.

## Configuration Refresh API

The `/config/refresh` endpoint, provided by the `config` component, is used to update a running {{ book.product }} instance when its block or service configuration files were modified through some means other than the `/blocks` and `/services` APIs. For example, if you use a text editor to modify a block configuration file, you need to tell the running {{ book.product }} instance to use those changes. You can do this with a GET request to the `/config/refresh` endpoint of your running instance.

    curl -XGET 'localhost:8181/config/refresh' --user 'Admin:Admin'
