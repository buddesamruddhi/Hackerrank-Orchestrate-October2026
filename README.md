# Ghost Data Still Exists: 

HackerRank Orchestrate, October 2026.

A deletion workflow can report **Complete** while a person's data still sits in replicas, search indexes, support
tickets, analytics, logs or backups, and sync or restore jobs can bring deleted data back. This agent audits every
request in `dataset/deletion_requests.csv` and decides, from the supplied evidence, whether the deletion is really
done:

- **`NOT_APPLICABLE`**: the request does not ask for deletion (access, correction, export, marketing opt-out, ...).
- **`COMPLETE`**: every copy has the treatment the policy requires. The output lists evidence-backed verification
  checks.
- **`INCOMPLETE`**: data or a recreation path remains. The output lists the findings, an ordered remediation plan,
  and the checks that must pass afterwards.

The result is written to `output.csv` (`case_id,deletion_status,steps_json`, 518 rows).

**Design principle:** deterministic Python does everything that can be computed exactly (parsing, identity, time,
policy, ordering). An LLM is used only where it adds something, as a **second gate** over multilingual request text
and application screenshots.

---


