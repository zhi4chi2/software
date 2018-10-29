credential.helper 的值

- default - not to cache at all. Every connection will prompt you for your username and password.
- cache - keeps credentials in memory for a certain period of time. None of the passwords are ever stored on disk, and they are purged from the cache after 15 minutes.
- store - saves the credentials to a plain-text file on disk, and they never expire. This means that until you change your password for the Git host, you won’t ever have to type in your credentials again.
- osxkeychain - In Mac, caches credentials in the secure keychain that’s attached to your system account.
- If you’re using Windows, you can install a helper called “Git Credential Manager for Windows.” This is similar to the “osxkeychain” helper described above, but uses the Windows Credential Store to control sensitive information. It can be found at <https://github.com/Microsoft/Git-Credential-Manager-for-Windows>.


FIXME

