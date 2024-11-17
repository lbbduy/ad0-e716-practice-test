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

<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Api/etc/extension_attributes.xsd">
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
- The fields used for the join are inverted reference_field should have contained `order_id` and `join_on_field` should have
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
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Cron: etc/crontab.xsd">
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
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn: magento: module:Magento_Cron: etc/crontab.xsd">
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
- Create a Dynamic Row system config using the `ArraySerialized` `backend_model` and a custom `frontend_model`.

_Choose 1 option._