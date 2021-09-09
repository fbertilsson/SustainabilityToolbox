# Implementation

## Minimize Storage using Azure Storage Management Policy

You can instruct Azure Storage to delete old data ore move to "cool" tier using a storage management policy. In Terraform it can look like this:

  ```tf
  resource "azurerm_storage_management_policy" "this" {
    storage_account_id = azurerm_storage_account.this.id

    rule {
      name    = "purge"
      enabled = true
      filters {
        blob_types   = ["blockBlob"]
      }
      actions {
        base_blob {
          tier_to_cool_after_days_since_modification_greater_than    = 7
          delete_after_days_since_modification_greater_than          = 31
        }
      }
    }
  }
  ```

## TODO write about

Periodic shutdown and scaling

* Runbooks in Azure
* ditto AWS
* ditto GC

Autoscaling
