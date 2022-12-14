# Implementation

## Minimize Storage using Azure Storage Management Policy

You can instruct Azure Storage to move to "cool" tier and/or delete old data using a storage management policy.

The below Terraform snippet creates a policy that does the following:

* Moves blobs to cool tier after a week
* Deletes blobs after a month

  ```tf
  resource "azurerm_storage_management_policy" "this" {
    storage_account_id = azurerm_storage_account.this.id

    rule {
      name    = "coolAndDelete"
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
