# Location and VPN Change What a Tester Sees

The **backend decides a user's country**, usually from the **IP address** of the request.

| Source                            | Used to decide the country? |
| --------------------------------- | --------------------------- |
| **IP address of the request**     | ✅ Yes (usually)            |
| **Device GPS**                    | ❌ No                       |
| **Country in account settings**   | ❌ No                       |

> **Anything that changes your IP changes what the app shows you.**

## Things That Change It

| Cause                              | What happens                                                                                          |
| ---------------------------------- | ----------------------------------------------------------------------------------------------------- |
| **VPN or proxy**                   | Makes you **appear to be in another country**                                                         |
| **Travelling or switching networks** | Can **change the apparent country**                                                                 |
| **Corporate or cloud networks**    | May route traffic out through a **different country** than the one you are physically in             |
| **IP lookup mistakes**             | The database that maps IPs to countries is **sometimes wrong**, or **has no answer**                  |
