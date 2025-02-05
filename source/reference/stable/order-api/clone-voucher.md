# Clone voucher

```eval_rst
.. api-name:: Order API
   :version: 1

.. endpoint::
   :method: PUT
   :url: *base*/voucher/*id*/clone

.. authentication::
   :api_key: true
```

This will clone a voucher with updated provided information

## Parameters

```eval_rst
.. list-table::
   :widths: auto

   * - ``name``

       .. type:: string
          :required: false

     - Name of the voucher.

   * - ``code``

       .. type:: string
          :required: false

     - Code of the voucher. Will be generated a random one if not passed.

   * - ``replaceExisting``

       .. type:: boolean
          :required: false

     - Default ``false``. Allow cloning to existing code. Will deactivate the existing voucher.

   * - ``stopDate``
   
       .. type:: string
          :required: true
   
     - Stop date of the voucher in ``Y-m-d`` format.

   * - ``conversionHtml``

       .. type:: string
          :required: false

     - Conversion html of the voucher

```

## Request example

```eval_rst
.. code-block:: http
   :linenos:

   PUT <base>/voucher/3/clone HTTP/1.1

   {
      "name": "Welcome 10%",
      "code": "new-welcome-10",
      "stopDate": "2022-07-09"
   }
```

```eval_rst
.. _order-api-clone-voucher-response:
```

## Response

`200` `Content-type: application/json`

```eval_rst
.. list-table::
   :widths: auto

   * - ``status``

       .. type:: string
          :required: true

     - ``ok`` if success, else ``no``.

   * - ``voucher``

       .. type:: int
          :required: false

     - Id of a new voucher

   * - ``code``

       .. type:: string
          :required: false

     - Code of a new voucher
```

## Response example

```eval_rst
.. code-block:: json
   :linenos:

   {
       "status": "ok",
       "voucher": 4,
       "code": "new-welcome-10"
   }

```
## Errors example

Required fields are not passed
```eval_rst
.. code-block:: json
   :linenos:

   {
       "status": "no",
       "voucher": "4",
       "msg": {
           "stopDate": "required"
       }
   }

```

Voucher not found
```eval_rst
.. code-block:: json
   :linenos:

   {
       "status": "no",
       "voucher": "3",
       "msg": {
           "voucher": "Voucher not found"
       }
   }

```

Auto vouchers not supported
```eval_rst
.. code-block:: json
   :linenos:

   {
       "status": "no",
       "voucher": "3",
       "msg": {
           "voucher": "Auto vouchers not supported"
       }
   }

```

Voucher does not belong to this store
```eval_rst
.. code-block:: json
   :linenos:

   {
       "status": "no",
       "voucher": "3",
       "msg": {
           "voucher": "Voucher does not belong to this store"
       }
   }

```

Voucher code already exists
```eval_rst
.. code-block:: json
   :linenos:

   {
       "status": "no",
       "voucher": "3",
       "msg": {
           "code": "Code is already taken"
       }
   }

```
