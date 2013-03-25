ACKeychain
==========

The easiest keychain wrapper for iOS.

ACKeychain requires the Security.framework in order to compile.

ACKeychain is a singleton and can be initalized easily.
 
Option A:

    ACKeychain *keychain = [ACKeychain defaultKeychain];
    
Option B:

	[[ACKeychain defaultKeychain] …];
	
Storing credentials:
    
    // Save credentials for user1
    if ([[ACKeychain defaultKeychain] storeUsername:@"user1" password:nil identifier:@"account1" forService:@"twitter"]) {
        NSLog(@"SAVED credentials for username 'user1' credentials identifier 'account1'");
    }

    // Save credentials for user2
    if ([[ACKeychain defaultKeychain] storeUsername:@"user2" password:@"password" identifier:@"account2" forService:@"twitter"]) {
        NSLog(@"SAVED credentials for username 'user2' credentials identifier 'account2'");
    }

    // Replace user2 with user3
    if ([[ACKeychain defaultKeychain] storeUsername:@"user3" password:@"password" identifier:@"account2" forService:@"twitter"]) {
        NSLog(@"CHANGED credentials for credentials identifier 'account2'");
    }    
    
    
Retrieving credentials:
    
    // Request all credentials for service 'twitter' (max 99 entries)
    NSArray *all = [[ACKeychain defaultKeychain] allCredentialsForService:@"twitter" limit:99];
    NSLog(@"All credentials for service 'twitter %@", all);

    // Request credentials for account with username 'user1'
    NSDictionary *credentials = [[ACKeychain defaultKeychain] credentialsForUsername:@"user1" service:@"twitter"];
    NSLog(@"CREDENTIALS: service: %@, identifier: %@, username: %@, password: %@",
        [credentials valueForKey:ACKeychainService],
        [credentials valueForKey:ACKeychainIdentifier],
        [credentials valueForKey:ACKeychainUsername],
        [credentials valueForKey:ACKeychainPassword]);

    // Request credentials for account with identifier 'account2'
    credentials = [[ACKeychain defaultKeychain] credentialsForIdentifier:@"account2" service:@"twitter"];
    NSLog(@"CREDENTIALS: service: %@, identifier: %@, username: %@, password: %@",
        [credentials valueForKey:ACKeychainService],
        [credentials valueForKey:ACKeychainIdentifier],
        [credentials valueForKey:ACKeychainUsername],
        [credentials valueForKey:ACKeychainPassword]);

Removing credentials:
    
    // Delete credentials for account with identifier 'account1'
    if ([[ACKeychain defaultKeychain] deleteCredentialsForIdentifier:@"account1" service:@"twitter"]) {
        NSLog(@"DELETED credentials for 'account1'");
    }

    // Request credentials for account with username 'user3'
    if ([[ACKeychain defaultKeychain] deleteCredentialsForUsername:@"user3" service:@"twitter"]) {
        NSLog(@"DELETED credentials for 'user3'");
    }

    // Delete all account for service MobileMe
    if ([[ACKeychain defaultKeychain] deleteAllCredentialsForService:@"MobileMe"]) {
        NSLog(@"DELTED all credentials for service 'MobileMe'");
    }
