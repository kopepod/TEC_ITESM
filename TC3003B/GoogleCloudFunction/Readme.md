# Google Cloud Function Tutorial

1. Go to (May/2024) : https://console.cloud.google.com/functions
2. Click on _Create function_
3. Fill Enviorment/Function-name/Region and Allow unauthenticated invocations
4. Select Runtime
5. Click on _Deploy_
6. Select Permissions TAB
7. CLick on _GRANT ACCESS_
8. Add **allUsers** to New princials
9. Select **Cloud Functions Invoker** for Role
10. Test with Curl

```bash
curl -m 70 -X POST https://<site>.cloudfunctions.net/<function> -H "Content-Type: application/json" -d '{"message": "Hello World There"}'
```
