JPA Relationship Summary (ManyToOne / OneToMany / Cascade / OrphanRemoval)

1) Foreign Key Location
- The foreign key column always exists on the @ManyToOne side.
- If Kid has @ManyToOne Parent, then the "kid" table contains:
      parent_id  → this is the real foreign key column.
- The database only stores the parent’s ID (not the object).

2) @JoinColumn
- Defines the foreign key column name.
- Example meaning:
      @JoinColumn(name = "parent_id")
  → Create/use column named parent_id.
- If omitted, Hibernate auto-generates a default column (usually parent_id).

3) @ForeignKey(name = "fk_kid_parent")
- ONLY names the database constraint.
- Does NOT create a new column.
- Does NOT change logic.
- Without it, Hibernate generates a random constraint name.
- Used for clean schema and easier debugging.

4) Ownership Rule
- @ManyToOne is ALWAYS the owning side.
- The foreign key lives there.
- @OneToMany(mappedBy = "parent") is the inverse side.
- Relationship is controlled from the @ManyToOne side.

5) cascade = {CascadeType.PERSIST, CascadeType.MERGE}
Means:
- Persist parent → children are saved automatically.
- Merge (update) parent → children are updated automatically.
- Remove parent → children are NOT deleted.
- Refresh/Detach → NOT cascaded.

This setup:
✔ Auto save
✔ Auto update
❌ No automatic delete (safer for production)

6) cascade = CascadeType.ALL
Includes:
- PERSIST
- MERGE
- REMOVE
- REFRESH
- DETACH

Important effect:
- Removing parent → all children are deleted automatically.
⚠ Can be dangerous (accidental mass deletion).

7) orphanRemoval = true
- If a child is removed from the parent’s collection:
      → JPA deletes that child from the database.
- Without orphanRemoval:
      → parent_id becomes NULL
      → child still exists in DB.

8) JPA Cascade vs Database ON DELETE CASCADE

JPA Cascade:
- Handled by Hibernate/Java.
- Happens before SQL execution.
- Requires EntityManager.

Database ON DELETE CASCADE:
- Handled directly by database.
- Works even outside the application.
- Usually faster for large datasets.

FINAL KEY IDEAS:
- parent_id is the real foreign key.
- @JoinColumn defines the column.
- @ForeignKey names the constraint.
- {PERSIST, MERGE} = safe automatic save/update.
- ALL includes REMOVE and can be risky.
- orphanRemoval deletes children when removed from collection.
---
1) Ownership and Cascade Are Different Concepts

Ownership:
- Determines where the foreign key lives.
- @ManyToOne is always the owning side.
- @OneToMany(mappedBy=...) is the inverse side.

Cascade:
- Controls which operations propagate (persist, merge, remove, etc.).
- It has nothing to do with foreign key ownership.
---
2) Can cascade be placed on the inverse side (@OneToMany)?

YES.

Example:
Parent
  @OneToMany(mappedBy="parent", cascade=ALL)

Kid
  @ManyToOne

---
5. Where should cascade usually be placed?
    

Best practice:

✔ Put cascade on the parent side (@OneToMany)  
✔ Avoid cascade REMOVE on @ManyToOne

Why?

If you put REMOVE on @ManyToOne:

remove(kid)  
→ might delete parent  
→ which might delete all other kids

This can cause chain deletion disasters.

---
JPA OneToMany / ManyToOne Best Practice Summary

1) Current setup:
   - @OneToMany with cascade = {PERSIST, MERGE}, orphanRemoval = true
   - @ManyToOne without cascade

2) Behavior:
   - Adding a child to parent → child automatically saved (PERSIST)
   - Updating a child through parent → child automatically updated (MERGE)
   - Removing a child from parent's collection → child is deleted from DB (orphanRemoval = true)
   - Deleting parent → children are NOT deleted automatically (REMOVE not included), likely causes ConstraintViolationException if still referenced

3) Why this setup is preferred:
   - Prevents accidental mass deletion
   - Forces explicit handling of parent deletion
   - Collection-level removal works safely
   - Maintains database integrity
   - Intent is clear to other developers

4) Trade-offs:
   - Safer: parent deletion must be handled manually → more control
   - If business rules require deleting parent along with children → include REMOVE cascade or CascadeType.ALL
   - Avoid cascade REMOVE on @ManyToOne → can accidentally delete parent when deleting child

5) Architectural guideline:
   - If parent is an aggregate root and children should not exist independently → consider REMOVE cascade
   - If children may exist independently → avoid REMOVE, handle deletion explicitly

6) Summary:
   - Cascade PERSIST + MERGE → automatic save/update
   - orphanRemoval = true → automatic child deletion when removed from collection
   - Cascade REMOVE → only use when business rules require parent deletion to remove children
   - Manual handling of parent deletion with current setup is safer and recommended for loosely coupled relationships
