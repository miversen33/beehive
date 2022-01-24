# Beehive

Beehive is a decentralized governance based job scheduling and remote job execution manager
<!-- Thats alot of jargon, break that down -->

## Buzz Protocol

Bees can communicate via the [`Buzz` protocol](#buzz-protocol), which is meant to be one way communication, and is defined as

`bz:\\$BEE_ID\$BEE_GENERATED_KEY\$BEEHIVE_PROVIDED_KEY\$ACTION\$HONEYCOMB`

Buzz communication should always have a header that is exactly $HEADER_SIZE bits long. Buzz messages must always be under $BUZZ_SIZE_LIMIT bits long

A breakdown of what each variable in the above protocol schema is

### $BEE_ID
    
    A bee should generate a seeded ID that is both unique and consistent to _something_ about the Bee. This will help the hive identify it overtime

### $BEE_GENERATED_KEY
    
    A bee will generate an acceptance key upon initialization. This key will be provided via STDOUT from the `[$INIT_COMMAND](#bee-initialization)` command, and can also be retrieved via the `[$KEY_RETRIEVAL_COMMAND](#bee-key-retrieval)`. A Bee's key can be changed, should it need to be, via the `[$KEY_UPDATE_COMMAND](#bee-key-update)`
    - Bee Keys must be matchable via the following regex `/[A-Za-z0-9_\-]+/`
    - Bee Keys are used as a way to identify itself (uniquely) within the beehive it is a part of
    - See also [Bee initialization](#bee-initialization), [Bee Key Retrieval](#bee-key-retrieval), [Bee Key Update](#bee-key-update)

### $BEEHIVE_PROVIDED_KEY
    
    The beehive will provide a key to any new bee that is accepted into the hive. This key is irretrivable, and as such should not be lost. The key is also unique per member of the hive, to promote security and bee safety
    - Beehive Keys must be matchable via the following regex `/[A-Za-z0-9_\-]+/`
    - See also [Beehive Connecting](#bee-hive-connection)

### $ACTION
    The listed action to perform. [There are a few predefined actions](#buzz-actions).
    Note: Actions can be locked behind various means of restriction. See [Action Locks](#action-locks)
    Note: Actions are _not_ case sensitive
    - [enter](#action-enter)
    - [exit](#action-exit)
    - [get_actions](#action-get-actions)
    - [submit_action](#action-submit-action)
    - [get_bee_count](#action-get-bee-count)
    - [update](#action-update)
    - [inform_missing](#action-inform-missing)
    - [update_action](#action-update-action) See also [Action Locks](#action-locks)
    
#### Action Locks
    
    Actions can be restriced on a variety of identifiers. These restrictions are set at beehive initialization and _cannot_ be changed once the beehive has more than 1 active bee member
    - Network Device (NIC)
    - IP Address/Range Mask
    - Custom Key

#### Action Enter
    
    - Return Honeycomb
        - [BEEHIVE_PROVIDED_KEY](#BEEHIVE_PROVIDED_KEY): String
    As Bee's cannot just enter a hive on their own, a known, **accepted** Bee must nominate a new Bee to the hive.
        A Bee recieves an [enterance request from another bee (#action-enter). The Bee checks the blacklist for the requesting Bee's ID, Key, Server Key (if provided), and IP address. If any of this is found in the blacklist, the Bee's nomination should be rejected and the TTL (time to live) for the rejection is reset to the predefined Rejection TTL.
        If the Bee's info is not found in the blacklist, a generated [BEEHIVE_PROVIDED_KEY](#BEEHIVE_PROVIDED_KEY) is provided. The Bee is then admitted to the hive

#### Action Exit
    
    - Honeycomb Definition
        - TODO (FILL ME IN?) 
    A Bee calls `exit` when they are leaving the hive. If data is stored within the Bee, that data should be provided within the optional Honeycomb

#### Action Get Actions

#### Action Submit Action

#### Action Get Bee Count

#### Action Update

#### Action Inform Missing

### $HONEYCOMB

## Beehive Standard

## Honeycomb Format
