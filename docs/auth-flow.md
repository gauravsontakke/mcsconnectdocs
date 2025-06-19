## Authentication Flow

1. Login via `/rest/auth/tokens`
2. Store JWT token securely in Flutter (preferably `flutter_secure_storage`)
3. Pass token in `Authorization: Bearer <token>` header
4. Logout simply deletes the token client-side