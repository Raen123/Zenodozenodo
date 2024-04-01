asyncapi: 2.6.0
defaultContentType: json
info:
  title: 3xpl.com Websockets API
  version: 0.5.1
  contact:
    name: 3xpl.com
    url: https://www.3xpl.com/
    email: 3@3xpl.com
  description: >
    3xpl.com WebSockets API provide real-time data coming from blockchains.


    You can quickly play with the API using
    [websocat](https://github.com/vi/websocat#installation) like this:

    ```bash

    websocat wss://stream.3xpl.net/ -S

    ```
externalDocs:
  url: https://3xpl.com/data/websocket-api
servers:
  websockets:
    url: stream.3xpl.net
    protocol: wss
    description: >-
      The Public Beta server available without authorization. Once the connection is established you can subscribe to a public channel by sending a subscribe request message.

channels:
  {blockchain}/blocks:
    parameters:
      blockchain:
        description: |
          id of blockchain to receive blocks from
        schema:
          type: string
          $ref: '#/components/schemas/blockchain'
    subscribe:
      summary: Stream information about new blocks in blockchain
      message:
        $ref: '#/components/messages/blocks'
  {blockchain}/events:
    parameters:
      blockchain:
        description: id of blockchain to receive events from
        schema:
          type: string
          $ref: '#/components/schemas/blockchain'
    subscribe:
      summary: Stream information about new events in blockchain
      message:
        $ref: '#/components/messages/events'
  {blockchain}/mempool:
    parameters:
      blockchain:
        description: id of blockchain to receive events from
        schema:
          type: string
          $ref: '#/components/schemas/blockchain'
    subscribe:
      summary: >-
        Stream information about new events in mempool (if specified blockchain
        supports it)
      message:
        $ref: '#/components/messages/mempool'
  {blockchain}/transaction/{hash}:
    parameters:
      blockchain:
        description: id of blockchain to receive events from
        schema:
          type: string
          $ref: '#/components/schemas/blockchain'
      hash:
        description: Transaction hash
        schema:
          type: string
    subscribe:
      summary: Receive event when a mempool transaction will be included in the block
      message:
        $ref: '#/components/messages/transaction'
  {blockchain}/address/{hash}:
    parameters:
      blockchain:
        description: id of blockchain to receive events from
        schema:
          type: string
          $ref: '#/components/schemas/blockchain'
      hash:
        description: Address
        schema:
          type: string
    subscribe:
      summary: Stream information about new events address affected
      message:
        $ref: '#/components/messages/address'
  {blockchain}/currency/{hash}:
    parameters:
      blockchain:
        description: id of blockchain to receive events from
        schema:
          type: string
          $ref: '#/components/schemas/blockchain'
      hash:
        description: Currency contract address
        schema:
          type: string
    subscribe:
      summary: Stream information about new events with provided currency
      message:
        $ref: '#/components/messages/events'
components:
  messages:
    blocks:
      summary: Message with block data information.
      description: |
        Message cointains information about new blocks in specified blockchain
      payload:
        $ref: '#/components/schemas/blocks'
      examples:
        - name: Bitcoin block number 500000
          summary: ''
          payload:
            data:
              - block: 500000
                hash: >-
                  00000000000000000024fb37364cbf81fd49cc2d51c09c75c35433c3a1945d04
                time: '2017-12-18T18:35:25.000000Z'
                events:
                  bitcoin-main: 13340
                  bitcoin-omni: 420
            context:
              time: 0.59455600 1685039844
    events:
      summary: Message with new events
      description: Stream real-time information about new events in blockchain
      payload:
        $ref: '#/components/schemas/events'
      examples:
        - name: First events in Bitcoin blockchain
          summary: ''
          payload:
            data:
              - blockchain: bitcoin
                module: bitcoin-main
                block: 0
                transaction: 4a5e1e4baab89f3a32518a88c31bc87f618f76673e2cc77ab2127b7afdeda33b
                sort_key: 0
                address: the-void
                currency: bitcoin
                effect: '-5000000000'
                failed: false
                extra: null
                extra_indexed: null
              - blockchain: bitcoin
                module: bitcoin-main
                block: 0
                transaction: 4a5e1e4baab89f3a32518a88c31bc87f618f76673e2cc77ab2127b7afdeda33b
                sort_key: 1
                address: 1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa
                currency: bitcoin
                effect: '+5000000000'
                failed: false
                extra: null
                extra_indexed: null
            context:
              time: '2023-03-02T18:24:51.000000Z'
    mempool:
      summary: Message with new events
      description: >
        Stream cointains real-time information about new events in mempool (if
        available)
      payload:
        $ref: '#/components/schemas/mempool-events'
      examples:
        - name: First events in Bitcoin blockchain
          summary: ''
          payload:
            data:
              - blockchain: bitcoin
                module: bitcoin-main
                block: -1
                transaction: 63381b941dbe21d6b7d03cab158118d74c7c313eb4c9164abf64f1293702923a
                sort_key: 326
                address: bc1qkcwtu2k9jjhyvlx804xx5ae786yksqhvju46ml
                currency: bitcoin
                effect: '-723449'
                failed: false
                extra: null
                extra_indexed: null
              - blockchain: bitcoin
                module: bitcoin-main
                block: -1
                transaction: 63381b941dbe21d6b7d03cab158118d74c7c313eb4c9164abf64f1293702923a
                sort_key: 325
                address: bc1qph5wssklxwsl50vyhstlg232nzqwp8sfws2zqm
                currency: bitcoin
                effect: '-910585'
                failed: false
                extra: null
                extra_indexed: null
            context:
              time: '2023-03-02T16:20:00.000000Z'
    transaction:
      summary: Message with new events
      description: Stream event when a mempool transaction is included in the block
      payload:
        $ref: '#/components/schemas/transaction'
      examples:
        - name: First transaction in Dogecoin blockchain
          summary: ''
          payload:
            data:
              module: dogecoin-main
              block: 0
              transaction: 5b2a3f53f605d62c53e62932dac6925e3d74afa5a4b459745c36d42d0ed26a69
              time: '2013-12-06T10:25:40.000000Z'
            context:
              time: '2013-12-06T10:25:40.000000Z'
    address:
      summary: Message with new events associated with address
      description: Stream contains events which affect the address
      payload:
        $ref: '#/components/schemas/events'
      examples:
        - name: Some recently events affected to first address in Bitcoin blockchain
          summary: ''
          payload:
            data:
              - blockchain: bitcoin
                module: bitcoin-main
                block: 779007
                transaction: 685e1c7bd823384335e1b3519148622e97a6e6a637bfee339c347e1d994b73bc
                sort_key: 13093
                time: '2023-03-02T18:38:33.000000Z'
                currency: bitcoin
                effect: '+7491'
                failed: false
                extra: null
                extra_indexed: null
              - blockchain: bitcoin
                module: bitcoin-main
                block: 779006
                transaction: 6783e8ef51befa0eb31f12c7e36317ceca1f766f0c7ce2af5c13ede7cffc43de
                sort_key: 1918
                time: '2023-03-02T18:24:51.000000Z'
                currency: bitcoin
                effect: '+7047'
                failed: false
                extra: null
                extra_indexed: null
            context:
              time: '2023-03-02T18:24:51.000000Z'
  schemas:
    block:
      type: object
      description: Block object
      properties:
        block:
          type: integer
          description: Block identifier
        hash:
          type: string
          description: Block hash
        time:
          type: string
          description: Timestamp when block issued
        events:
          type: object
          description: Key-value object with events count by module
          properties:
            '{:module}':
              type: integer
              description: Events count
        additionalProperties: false
      required:
        - block
        - hash
        - time
        - events
    blocks:
      type: object
      description: ''
      properties:
        data:
          type: array
          description: List of blocks
          items:
            type: object
            $ref: '#/components/schemas/block'
        context:
          type: object
          properties:
            time:
              type: string
              description: Time when message was produced
            additionalProperties: true
      additionalProperties: false
    blockchain:
      type: string
      enum:
        - bitcoin
        - ethereum
        - bitcoin-cash
        - bnb
        - dogecoin
        - litecoin
        - ton
    events:
      type: object
      description: ''
      properties:
        data:
          type: array
          description: List of events
          items:
            type: object
            $ref: '#/components/schemas/event'
            additionalProperties: false
        context:
          type: object
          properties:
            time:
              type: string
              description: Time when message was produced
            additionalProperties: true
      additionalProperties: false
    event:
      type: object
      description: Event object
      properties:
        blockchain:
          type: string
          $ref: '#/components/schemas/blockchain'
        module:
          type: string
          description: Module in which the event occurred
        block:
          type: integer
          description: Number of block in which the event included
        transaction:
          type: string
          description: Hash of transaction contains the event
        sort_key:
          type: integer
          description: Sorting number
        address:
          type: string
          description: Address affected by the event
        currency:
          type: string
          description: Effect currency
        effect:
          type: string
          description: Amount in currency which address effected
        failed:
          type: boolean
          description: Shows is event failed by any reason
        extra:
          type: 'null'
          description: ''
        extra_indexed:
          type: 'null'
          description: ''
    mempool-events:
      type: object
      description: ''
      properties:
        data:
          type: array
          description: List of mempool events
          items:
            type: object
            $ref: '#/components/schemas/mempool-event'
            additionalProperties: false
        context:
          type: object
          properties:
            time:
              type: string
              description: Time when message was produced
            additionalProperties: true
      additionalProperties: false
    mempool-event:
      type: object
      description: Mempool event object
      properties:
        blockchain:
          type: string
          $ref: '#/components/schemas/blockchain'
        module:
          type: string
          description: Module in which the event occurred
        block:
          type: integer
          description: '`-1` always'
        transaction:
          type: string
          description: Hash of transaction contains the event
        sort_key:
          type: integer
          description: Sorting number
        address:
          type: string
          description: Address affected by the event
        currency:
          type: string
          description: Effect currency
        effect:
          type: string
          description: Amount in currency which address effected
        failed:
          type: boolean
          description: Shows is event failed by any reason
        extra:
          type: 'null'
          description: ''
        extra_indexed:
          type: 'null'
          description: ''
    transaction:
      type: object
      description: Transaction object
      properties:
        module:
          type: string
          description: Module in which the transaction processed
        block:
          type: integer
          description: Number of block in which the transaction included
        transaction:
          type: string
          description: Transaction hash
        time:
          type: string
          description: Transaction timestamp
