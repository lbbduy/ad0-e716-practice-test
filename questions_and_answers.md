### 1. An Adobe Commerce developer creates a custom router class.

### Which interface should the class implement?

- ```\Magento\Framework\App\Http\RouterInterface```
- ```\Magento\Framework\App\RouterInterface```    👈
- ```\Magento\Framework\App\RouterListInterface```

_Choose 1 option._

### 2. An Adobe Commerce developer is tasked with adding the parent order's increment id to creditmemos fetched through

```Magento\Sales\Model\Order\CreditmemoRepository```. To implement this, they choose to create an extension attribute
and use the join directive as follows:

```xml

<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Api/etc/extension_attributes.xsd">
    <extension_attributes for="Magento\Sales\Api\Data\CreditmemoInterface">
        <attribute code="order_increment_id" type="string">
            <join reference_table="sales_order" reference_field="entity_id" join_on_field="order_id">
                <field>increment_id</field>
            </join>
        </attribute>
    </extension_attributes>
</config>
```

### After a few tests, the developer realizes that the development is not working as expected and that the creditmemos fetched do not contain the increment id. What is the reason for this?

- The join directive for extension attributes does not exist so it is simply ignored by Magento and nothing gets added.
- The fields used for the join are inverted reference_field should have contained `order_id` and `join_on_field` should
  have
  contained `entity_id`.
- **The join directive only works for `getList()` calls, in this case the creditmemos are fetched using `get()`.** 👈

_Choose 1 option._

### 3. An Adobe Commerce developer is being tasked with disabling a cron job added by a third-party module. The developer has already created a new module with a dependency on the third-party

module:

```xml

<group id="default">
    <job name="reminder_email" instance="Vendor\Module\Model\ReminderEmail" method="execute">
        <schedule>0 0 ** *</schedule>
    </job>
</group>
```

### What would a developer do to disable the cron job?

- Rewrite the `reminder_email` cron job to add `disable="true"` to the job node.

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Cron: etc/crontab.xsd">
    <group id="default">
        <job name="reminder_email" instance="Vendor\Module\Model\ReminderEmail" method="execute" disable="true">
            <schedule>0 0 ** *</schedule>
        </job>
    </group>
</config>
```

- **Rewrite the `reminder_email` cron job schedule to run on a date that which will never occur.** 👇 👈

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn: magento: module:Magento_Cron: etc/crontab.xsd">
    <group id="default">
        <job name="reminder_email" instance="Vendor\Module\Model\ReminderEmail" method="execute">
            <schedule>0 0 30 2 *</schedule>
        </job>
    </group>
</config>
```

- Create a `crontab.xml` file and use a `referenceJob` node to add `disable="true"` to the `reminder_email` cron job.

```xml 
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn: magento:module:Magento_Cron: etc/crontab.xsd">
    <group id="default">
        <referenceJob name="reminder email" disable="true"/>
    </group>
</config>
```

_Choose 1 option._

### 4. An Adobe Commerce developer is tasked with disabling an existing observer for the wishlist_product_add_after event.

### What would be the recommended way to achieve this?

- **Create a new `events.xml` file, declare the same event and observer name, then add `disabled="true"`.** 👈
- Create an around plugin on the execute method of the observer instance and stop the execution.
- Create a preference on the observer instance and override the complete function to stop the execution.

_Choose 1 option._

### 5. An Adobe commerce merchant has a store with multiple product types. Specific content needs to be added only to the simple products.

### Which layout should a developer use to achieve this?

- **catalog_product_view_type_simple.xml** 👈
- catalog_product_type_simple.xml
- catalog_product_view.xml
- catalog_category_view_product_simple.xml

_Choose 1 option._

### 6. An Adobe Commerce developer is tasked by a client to create a system configuration to store information about their company's multiple social media profiles (Facebook, Twitter, Instagram, etc.). They want to be able to control both the name of the service, as well as the URL, to their profile/page on said service, as well as adding more themselves in the future.
### How would the developer create an optimum system configuration to accomplish this task?

- Create a text_json system config so they can enter `JSON` data directly.
- Create a separate text type system configuration for each social media platform.
- **Create a Dynamic Row system config using the `ArraySerialized` `backend_model` and a custom `frontend_model`.** 👈

_Choose 1 option._

### 7. A user issuing a request similar to GET

`<host>/rest/<store_code>/V1/products/<sku>` receives product information similar to the following:

```json
{
  "sku": "tshirt1",
  "price": "20.00",
  "description": "New JSmith design",
  "extension_attributes": {
    "logo size": "small"
  },
  "custom_attributes": {
    "artist": "James Smith"
  }
}
```

### They were expecting to include the stock status and quantity as part of the result.

### Why would this be missing from the response?

- The stock status is only returned for products that have `is_saleable` attribute as true.
- This needs to be done as a `POST` instead of `GET`.
- **This is an anonymous or unauthenticated user and they are not allowed to view this information. 👈**

_Choose 1 option._

### 8. A developer has built a custom module that introduces a new entity. A client reports that after saving the new entity value in the backend, the frontend page still contains an old value.

### How should the developer make sure that the frontend page shows the updated value?

- Layout files must have cacheable=false set on specific block `sections.xml` file must have defined routes where the
  cache should be cleared
- An implementation of `IdentityInterface` for the frontend block
- cache.xml file must have a definition to clear the cache automatically

_Choose 1 option._

### 9. Refer to the image of the website hierarchy.

![store themes](./images/store-themes.jpg)

### How many different themes can be configured in the shop based on this hierarchy?

- Three, because themes are applied per store level
- **Five, because themes are applied per store view level** 👈
- One, because only one theme is allowed in a single instance
- Two, because themes are applied only per website level

_Choose 1 option._

### 10. An Adobe Commerce developer is working on a site with a multi-store setup containing a main retail store, and a secondary B2B store. They would like the sales emails from the B2B store to use product image URLs from the retail store. To achieve this they have used a plugin on the URL generation method to call

`Emulation::startEnvironmentEmulation`, passing through the correct `$storeId` and `$area`.

### However, they find that the URLs B2B sales emails are unchanged, and no exceptions are being thrown. Given that email generation already uses area emulation, why is this?

- Only one level of emulation is permitted at any one time.
- Emulation does not effect URLs which are stored fully qualified against the product.
- The $force parameter required to override this needs to be provided.

_Choose 1 option._

### 11. An Adobe Commerce developer is writing an integration test and needs to initialize the \MyVendor\MyModule\Model\MyClass class in order to test its logic. The class has one constructor parameter:

`\Magento\Customer\Api\CustomerRepositoryInterface $customerRepository`

### The test class and the test method inside have been written and the test framework's object manager has been instantiated into the

`$objectManager` variable.

### How is the `MyClass` class initialized?

-  ```php 
    $repository = $objectManager->instantiatePreference(\Magento\Customer\Api\CustomerRepositoryInterface::class);
    $myClass = new \MyVendor\MyModule\Model\MyClass($repository); 
    ``` 
- ```php
  $repository =$this->getMockClass(\Magento\Customer\Api\CustomerRepositoryInterface::class);
  $myClass = $objectManager->create(\MyVendor\MyModule\Model\MyClass::class, ['customerRepository' => $repository]);
  ```
- ```php
  $myClass = $objectManager->create(\MyVendor\MyModule\Model\MyClass::class);
  ```
  ☝️

_Choose 1 option._

### 12. An Adobe Commerce developer is working on a notification module. `MyVendor\Notification\Block\GuestNotifications` and `MyVendor\Notification\Block\CustomerNotifications` blocks have parameter `$notification` of type `MyVendor\Notification\Api\NotificationRepositoryInterface.`
### The service contract `MyVendor\Notification\Api\NotificationRepositoryInterface` and its concrete implementation `MyVendor\Notification\Model\NotificationRepository` are created.
### How would the `MyVendor\Notification\Model\NotificationRepository` implement `MyVendor\Notification\Api\NotificationRepositoryInterface`?

- **Declare interface preference. The object manager uses this mapping to handle interface type parameter injection.** 👈
  ```xml
  <preference
      for="MyVendor\Notification\Api\NotificationRepositoryInterface" 
      type="MyVendor\Notification\Model\NotificationRepository"
  />
  ```
- Declare parameter preference for both `GuestNotifications` and `CustomerNotifications`.
  ```xml
  <type name="GuestNotifications">
    <arguments>
        <argument name="notification" xsi:type="interface">MyVendor\Notification\Model\NotificationRepository</argument>
    </arguments>
  </type>
  ...
  <type name="CustomerNotifications">
      <arguments>
          <argument name="notification" xsi:type="interface">MyVendor\Notification\Model\NotificationRepository</argument>
      </arguments>
  </type>
  ```
    
- Declare NotificationRepository as a virtual type for NotificationRepositoryInterface.
  ```xml
  <virtualType
    name="MyVendor\Notification\Model\NotificationRepository"
    type="MyVendor\Notification\Api\NotificationRepositoryInterface"
  />
  ```

_Choose 1 option._


### 13. An Adobe Commerce developer starts a project where inventory is going to be managed outside of Magento using a custom connector module. A decision has been made to completely remove all Magento modules related to inventory as the first step to improve application performance. Over 70 such modules were identified, starting with `magento/module-inventory` (`Magento_Inventory`) and ending with `magento/module-inventory-wishlist` (`Magento_InventoryWishlist`). The developer already ran the following command:
### `composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition myproject`
### How can the developer ensure that modules related to inventory modules are removed from the codebase before Magento gets installed?

- Run the following command and include all the necessary modules: `bin/magento module: uninstall Magento_Inventory, ... ,Magento_InventoryWishlist`
- Include the following node in the main `composer.json` file of the project including all the necessary modules and run `composer update`: 
  ```json
    "replace": {
      "magento/module-inventory": "*",
      ...
      "magento/module-inventory-wishlist": "*"
    }
  ```
  ☝️
- Update the `autoload` > `exclude-from-classmap` node with namespaces of the modules to remove in the main composer.json file and run `composer update`:
  ```json
  "autoload": {
    ...
    "exclude-from-classmap": [
      "Magento\\Inventory\\**,
      ...
      "Magento\\InventoryWishlist\\**,
      ...
    ],
    ...
  }
  ```

_Choose 1 option._

_Preference: https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/get-started/install-update#remove-inventory-management_


### 14. There is a task to fix the output script injection for the following line of a `.phtml` file. 
### `<div data-bind='settings: <?= $myJson ?>'></div>`
### As an Adobe Commerce developer, what should be the correct escape method to use for JSON code inside an HTML attribute?

- `<div data-bind='settings: <?= $escaper->escapeJs($myJson) ?>'></div>`
- `<div data-bind='settings: <?= $escaper->escapeJson($myJson) ?>'></div>`
- `<div data-bind='settings: <?= $escaper->escapeHtmlAttr($myJson) ?>'></div>` 👈

_Choose 1 option._


### 15. An Adobe Commerce developer is adding a new system configuration field to the admin area. The new field will be used to store sensitive data that will be encrypted in the database. How would the developer add a configuration field with these constraints?


- ```xml
  <field id="secret_data" type="password" translate="label" sortOrder="10" showInDefault="1" showInWebsite="1" showInStore="1">
      <label>Secret Data</label>
  </field>
  ```

- ```xml
  <field id="secret_data" type="obscure" translate="label" sortOrder="10" showInDefault="1" showInWebsite="1" showInStore="1">
    <label>Secret Data</label>
    <backend_model>Magento\Config\Model\Config\Backend\Encrypted</backend_model>
  </field>
  ```
  ☝️

- ```xml
  <field id="secret_data" type="encrypted" translate="label" sortOrder="10" showInDefault="1" showInWebsite="1" showInStore="1">
    <label>Secret Data</label>
    <backend_model>Magento\Config\Model\Config\Backend\Encrypted</backend_model>
  </field>
  ```

_Choose 1 option._


### 16. An Adobe Commerce developer has attached observer to the `sales_order_save_before` event. In the execute method of the observer the developer modifies order info and invokes `\Magento\Sales\Model\Order::save` method.
### What is the end result?

- Adobe Commerce will throw an exception.
- **It will cause a cyclical event loop.** 👈
- The order will be saved successfully.

_Choose 1 option._


### 17. An Adobe Commerce developer is assisting a junior developer on their team. The junior developer is trying to add an additional attribute to select for a product collection of a block that extends `\Magento\Catalog\Block\Product\ListProduct`. The developer has attempted to do this by creating a plugin to the block:
```php
public function afterToHtml(\Vendor\CustomCatalog\Block\Product\ListProduct $subject, $result) {
    $subject->addAttribute('custom_attribute');
    return $result;
}
```
### Why does this not work correctly?

- The plugin cannot return the `$result` argument because the developer is trying to modify the output. The developer should return `$subject->toHtml()` instead to ensure the updated markup is rendered.
- **The load method of the collection has already been called in the **block's_beforeToHtml** method, so the modification of the select statement was made too late.** 👈
- The `ListProduct` block does not contain an `addAttribute` method. Instead, the developer should have called `$subject->getProductCollection()->addAttributeToSelect('custom_attribute')`.

_Choose 1 option._


### 18. An Adobe Commerce developer has been asked to create a custom Page Builder content type to render a grid of tiles showing available categories that can be clicked to navigate to the resulting product listing page. This content type accepts parameters to determine which categories to display. The client has asked that the User be able to see the resulting tiles appear in the Stage after the settings on the content type have been saved.
### How can this be accomplished?

- Override the `afterObservablesUpdated` method of the `preview.js` file and call the `getPreview('content-type-name')` method from `Magento_PageBuilder/js/config`, where `content-type-name` is the name of the custom content type.
- **Create a renderer that implements `\Magento\PageBuilder\Model\Stage\RendererInterface` and use `di.xml` to add it to the renderers argument of `Magento\PageBuilder\Model\Stage\RendererPool`.** 👈
- Create a custom controller and layout to generate the resulting markup based on the provided parameters and call it via AJAX from the `preview.js` file.

_Choose 1 option._


### 19. A code audit revealed that a project contains an `Acme\Blog\CustomClass` that uses direct SQL queries:
```php

public function getBlogPostsData(string $postName, \Zend_Db_Adapter_Pdo_Mysql $connection): array
{
    //using direct SQL queries for performance
    return $connection->query("SELECT * FROM blog_post WHERE name LIKE $postName") ->fetchAll();
}
```
### Which two methods can be used to make the code resistant to SQL Injection attacks? (Choose two.):

- Refactor CustomClass to use `\Magento\Framework\DB\Adapter\AdapterInterface` instead of `\Zend_Db_Adapter_Pdo_Mysql` so Magento can apply built-in sanitization methods automatically: 
```php
public function getBlogPostsData(string $postName, \Magento\Framework\DB\Adapter\AdapterInterface $connection): array
{
  return $connection->query("SELECT * FROM blog_post WHERE name LIKE $postName")->fetchAll();
}
```

- Create a model, resource model and a collection. Refactor the class to include a collection factory and use the collection to load the data:
```php
public function getBlogPostsData(string $postName): array
{
  /** @var \Acme\Blog\Model\ResourceModel\BlogPost\Collection $collection */
  $collection = $this->collectionFactory->create();
  $collection->addFieldToFilter('name', ['like' => $postName]);
  return $collection->getItems();
}
```
☝️

- Use a prepared statement to sanitize the input:
```php
public function getBlogPostsData(string $postName, \Zend_Db_Adapter_Pdo_Mysql $connection): array
{
  return $connection->query("SELECT * FROM blog_post WHERE name LIKE ?", [$postName])->fetchAll();
}
```
☝️

- Sanitize the input by escaping HTML special characters using the `htmlspecialchars()` function:
```php
public function getBlogPostsData(string $postName, \Zend_Db_Adapter_Pdo_Mysql $connection): array
{
  return $connection->query("SELECT * FROM blog_post WHERE name LIKE htmlspecialchars($postName)") ->fetchAll();
}
```

_Choose 2 options._


### 20. A module contains the `\Vendor\Module\CustomValidatorPool` class and has an array of validator classes in the constructor.
### The following two validators are added in the module `etc/di.xml` file:
```xml
<type name="Vendor\Module\Model\CustomValidatorPool">
    <arguments>
        <argument name="validators" xsi:type="array">
            <item name="validator1" xsi:type="string">Vendor\Module\Model\Validator1</item>
            <item name="validator2" xsi:type="string">Vendor\Module\Model\Validator2</item>
        </argument>
    </arguments>
</type>
```
### There is also one validator added in the `etc/adminhtml/di.xml` file:

```xml
<type name="Vendor\Module\Model\CustomValidatorPool">
<arguments>
    <argument name="validators" xsi:type="array">
        <item name="validator2" xsi:type="string">Vendor\Module\Model\AdminSpecificValidator2</item>
    </argument>
</arguments>
</type>
```
### When `\Vendor\Module\CustomValidatorPool` gets instantiated in the `adminhtml` area, what will it contain in the validators property?
    
- An array with exactly two elements containing `validator1` item specified in `etc/di.xml` and `validator2` item specified in `etc/adminhtml/di.xml`:
```php
[
  'validator1' => {Vendor\Module\Model\Validator1}
  'validator2' => {Vendor\Module\Model\AdminSpecificValidator2}
]
```

- An array with exactly one element containing the validator specified in etc/adminhtml/di.xml:
```php
[
   'validator2' => {Vendor\Module\Model\AdminSpecificValidator2}
]
```
☝️

- An array with exactly three elements containing the validator1 and validator2 items specified in etc/di.xml and validator2 items specified in etc/adminhtml/di.xml
```php
[
   0 => {Vendor\Module\Model\Validator1},
   1 => {Vendor\Module\Model\Validator2},
   2 => {Vendor\Module\Model\AdminSpecificValidator2}
]
```

_Choose 1 option._

_Preference: https://magento.stackexchange.com/a/139912_


### 21. An Adobe Commerce developer is tasked with developing a module for a service that requires the creation of a .txt file in the document root of the site. The contents of this file are supposed to be updated daily with data regarding the products added during the day. The file is fetched by the service at 7PM. The production environment on which the module will be deployed is composed of two frontend servers.
### How can this be achieved by the developer?

- This cannot be done inside of Magento since the file is in the document root, server redirects will be needed to redirect to a regular custom controller in charge of generating the data on the fly.
- **This can be done inside of Magento by creating a router in `etc/frontend/di.xml` that will match the filename and internally redirect to a regular custom controller in charge of generating the data on the fly.** 👈
- This can be done inside of Magento by declaring a cron job in `etc/crontab.xml` of the module and the class that will prepare the contents of the file and write them in the text file in Magento's root folder everyday at 6PM.
    
_Choose 1 option._


### 22. Which scope do cron tasks execute in?
    
- Store
- **Store View** 👈
- Website

_Choose 1 option._