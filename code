def measure_latency_and_bandwidth(trace_file):
    latency_sum = 0
    num_transactions = 0
    bandwidth_sum = 0
    max_bandwidth = 0

    with open(trace_file, 'r') as file:
        for line in file:
            timestamp, txn_type, data = line.strip().split()

            if txn_type == 'Rd':
                # Assuming timestamp for 'Data' indicates completion of read transaction
                latency = int(timestamp) - previous_timestamp
                latency_sum += latency
                num_transactions += 1

            elif txn_type == 'Wr':
                # Assuming all writes complete in one cycle
                bandwidth_sum += len(data)  # Assuming each byte transferred counts towards bandwidth

            previous_timestamp = int(timestamp)

            # Update max_bandwidth
            if bandwidth_sum > max_bandwidth:
                max_bandwidth = bandwidth_sum

    average_latency = latency_sum / num_transactions if num_transactions > 0 else 0
    average_bandwidth = max_bandwidth / previous_timestamp  # Assuming time stamps are in cycles

    return average_latency, average_bandwidth


