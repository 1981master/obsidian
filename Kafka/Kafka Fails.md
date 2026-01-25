🔥 Kafka failure scenarios (broker crash, rebalance)

Perfect — **this topic is pure senior / bank-grade Kafka knowledge**.  
Below is a **deep, scenario-based breakdown**, **failure → what happens → how banks handle it**.

---

# 🔥 Kafka Failure Scenarios (Broker Crash, Rebalance, Data Safety)

---
```java
import org.apache.kafka.clients.consumer.ConsumerRecord;
import org.springframework.kafka.annotation.KafkaListener;
import org.springframework.kafka.support.Acknowledgment;
import org.springframework.stereotype.Service;

@Service
public class TransactionConsumer {

    @KafkaListener(
        topics = "transactions",
        groupId = "bank-group"
    )
    public void consume(ConsumerRecord<String, String> record,
                        Acknowledgment ack) {

        // 1️⃣ CONSUME
        String message = record.value();
        String transactionId = record.key();

        // 2️⃣ PROCESS
        if (isDuplicate(transactionId)) {
            // already processed → skip but commit offset
            ack.acknowledge();
            return;
        }

        // 3️⃣ PERSIST (database operations)
        saveTransaction(transactionId, message);
        saveAuditLog(transactionId);

        // 4️⃣ COMMIT OFFSET (only after success)
        ack.acknowledge();
    }

    private boolean isDuplicate(String transactionId) {
        // check in DB / cache (idempotency)
        return false;
    }

    private void saveTransaction(String transactionId, String data) {
        // insert/update transaction table
    }

    private void saveAuditLog(String transactionId) {
        // insert audit record
    }
}

```
---

## 1️⃣ Broker Crash (MOST COMMON)

### Scenario

- Broker hosting **partition leader** crashes
    

---

### What Kafka Does

1. ZooKeeper / KRaft detects broker failure
    
2. Leader election happens
    
3. ISR replica becomes new leader
    
4. Producers/consumers reconnect
    

---

### What Happens to Messages?

|Case|Result|
|---|---|
|`acks=all` + ISR|No data loss|
|`acks=1`|Possible data loss|
|Leader not in ISR|Unclean election risk|

---

### Bank Best Practice

`acks=all min.insync.replicas=2 unclean.leader.election.enable=false`

✔ No message loss  
✔ Sacrifices availability for safety

---

## 2️⃣ Producer Failure During Send

### Scenario

- Producer sends message
    
- Network issue / crash before ACK
    

---

### Result

- Producer retries
    
- Message may be duplicated
    

---

### Bank Handling

- Idempotent producer
    
- Transactional producer
    

`enable.idempotence=true`

✔ Duplicate prevention  
✔ Safe retries

---

## 3️⃣ Consumer Crash BEFORE Offset Commit

### Scenario

- Consumer processes message
    
- Crashes before commit
    

---

### Result

- Offset not committed
    
- Message reprocessed
    

---

### Bank Handling

- At-least-once delivery
    
- Idempotent consumers
    

✔ No data loss  
✔ Possible duplicates handled

---

## 4️⃣ Consumer Crash AFTER Offset Commit

### Scenario

- Offset committed
    
- Business logic not finished
    

---

### Result

- Message LOST
    

---

### Bank Rule

❌ **Never commit offset before business logic**

---

### Correct Order

`Consume → Process → Persist → Commit Offset`
```java
@KafkaListener(topics = "transactions", groupId = "bank-group")
public void consume(ConsumerRecord<String, TransactionEvent> record,
                    Acknowledgment ack) {

    // 1️⃣ Consume
    TransactionEvent event = record.value();

    // 2️⃣ Process
    Account account = accountService.validateAndPrepare(event);

    // 3️⃣ Persist (DB transaction)
    accountRepository.save(account);
    auditRepository.save(new AuditLog(event.getId()));

    // 4️⃣ Commit Offset (only after successful persist)
    ack.acknowledge();
}

```
---

## 5️⃣ Consumer Group Rebalance (VERY IMPORTANT)

### Scenario

- New consumer joins
    
- Consumer leaves
    
- Partition reassignment happens
    

---

### What Happens

- Consumers pause
    
- Partitions revoked
    
- Offsets reloaded
    
- Processing resumes
    

---

### Risks

- Duplicate processing
    
- In-flight message loss
    
- Long pauses
    

---

### Bank Best Practices

#### ✔ Manual offset commit

`enable.auto.commit=false`

#### ✔ Commit offsets BEFORE rebalance

Use `ConsumerRebalanceListener`

---

### Rebalance-Safe Pattern

`onPartitionsRevoked:   commit offsets  onPartitionsAssigned:   resume processing`

---

## 6️⃣ Long Processing Causes Rebalance (Hidden Trap)

### Scenario

- Message processing takes long
    
- Poll not called in time
    

---

### Kafka Assumes

> Consumer is dead

---

### Result

- Rebalance triggered
    
- Duplicate processing
    

---

### Bank Fix

`max.poll.interval.ms = HIGH max.poll.records = LOW`

✔ Smaller batches  
✔ Faster polling

---

## 7️⃣ Broker Crash DURING Transaction

### Scenario

- Transactional producer crashes mid-transaction
    

---

### Kafka Behavior

- Transaction is aborted
    
- Uncommitted messages invisible
    
- Exactly-once preserved
    

---

### Consumer Sees

- Only committed messages
    
- Aborted messages skipped
    

---

## 8️⃣ Controller Crash (Kafka KRaft / ZooKeeper)

### Scenario

- Controller fails
    

---

### Kafka Reaction

- New controller elected
    
- Metadata refreshed
    
- Temporary pause
    

---

### Bank Impact

✔ No data loss  
✔ Short unavailability

---

## 9️⃣ Network Partition (Split Brain)

### Scenario

- Network split
    
- ISR shrinks
    

---

### Risk

- If `min.insync.replicas` not met → producer errors
    

---

### Bank Choice

✔ Fail fast  
✔ Preserve consistency

---

## 🔟 Disk Failure on Broker

### Scenario

- Disk corruption or full disk
    

---

### Kafka Action

- Broker goes offline
    
- Replica promoted
    

---

### Bank Rule

✔ Monitoring  
✔ Alerts  
✔ Capacity planning

---

## 🔥 COMMON BANK INTERVIEW QUESTIONS (WITH ANSWERS)

---

### Q: How do you prevent data loss in Kafka?

**A:**

- `acks=all`
    
- Replication factor ≥ 3
    
- Disable unclean leader election
    

---

### Q: How do you prevent duplicate processing?

**A:**

- Idempotent producer
    
- Idempotent consumer
    
- Deduplication store
    

---

### Q: What causes rebalancing?

**A:**

- Consumer join/leave
    
- Poll timeout
    
- Partition changes
    

---

### Q: What is ISR?

**A:**

- In-Sync Replicas
    
- Fully caught-up replicas eligible for leader
    

---

### Q: Why banks prefer consistency over availability?

**A:**

- Financial correctness
    
- Regulatory requirements
    

---

## 🏦 FINAL BANK-LEVEL SUMMARY (SAY THIS)

> “Kafka is designed for at-least-once delivery. In banking systems we prioritize consistency using acks=all, ISR, idempotent producers, and idempotent consumers. We handle failures through controlled rebalancing and fail-fast strategies rather than risking data corruption.”

where is ack variable came from where it declared

Good question — **this is a very common interview follow-up** 👍  
Let’s be precise and simple.

---

## Where does `ack` come from?

`ack` is **injected by Spring Kafka**, it is **not something you create manually**.

### Type

`org.springframework.kafka.support.Acknowledgment`

---

## How Spring provides it

When you use **manual acknowledgment mode**, Spring Kafka automatically passes an  
`Acknowledgment` object **as a method parameter** to your `@KafkaListener`.

That’s why you see it **directly in the method signature**:

`public void consume(ConsumerRecord<String, TransactionEvent> record,                     Acknowledgment ack)`

You do **NOT** declare it anywhere else.

---

## REQUIRED configuration (IMPORTANT)

Manual ack only works if you configure the container like this:

`spring.kafka.consumer.enable-auto-commit=false spring.kafka.listener.ack-mode=manual`

OR

`spring.kafka.listener.ack-mode=manual_immediate`

---

## What `ack.acknowledge()` really does

`ack.acknowledge();`

➡ Commits the **current record’s offset** to Kafka  
➡ Marks the message as **successfully processed**  
➡ Prevents reprocessing on restart or rebalance

---

## What happens if you DON’T call `acknowledge()`?

- Offset is NOT committed
    
- Message will be **re-consumed**
    
- This is **intentional** for failure recovery
    

---

## Bank-style explanation (say this in interview)

> “`Acknowledgment` is provided by Spring Kafka when manual commit mode is enabled.  
> It allows us to commit offsets only after business logic and database persistence succeed, ensuring at-least-once delivery with no message loss.”

---

## Minimal full example (for clarity)

`@KafkaListener(topics = "transactions", groupId = "bank-group") public void consume(ConsumerRecord<String, String> record,                     Acknowledgment ack) {      // process     saveToDatabase(record.value());      // commit offset manually     ack.acknowledge(); }`