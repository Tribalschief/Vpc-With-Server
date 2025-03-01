![Deployment Architecture](vpc-example-private-subnets.png)

# Vpc-With-Server
Implementation Steps
1. Virtual Private Cloud Setup
Console: AWS VPC Dashboard

1. Choose "VPC and more" configuration
2. Set Name Tag (e.g., `Prod-VPC`)
3. IPv4 CIDR: 10.0.0.0/16 (default)
4. Enable IPv6 if required
5. Availability Zones: 2
6. Subnets:
   - Public: 2 (10.0.0.0/24, 10.0.1.0/24)
   - Private: 2 (10.0.2.0/24, 10.0.3.0/24)
7. NAT Gateways: 1 per AZ
8. S3 Gateway Endpoint: Enabled
9. Disable DNS hostnames
2. Application Deployment
Auto Scaling Configuration

- Create Launch Template with AMI/configuration
- Configure Auto Scaling Group:
  - Min: 2, Desired: 3, Max: 5
  - Multi-AZ placement
- Attach Application Load Balancer
- Health Checks: HTTP:80/
3. Validation & Testing

1. Verify instance health in EC2 console
2. Test load balancer DNS endpoint
3. Use VPC Reachability Analyzer
4. Validate private subnet internet access
4. Resource Cleanup
Termination Sequence

Delete Auto Scaling Group

Remove Load Balancer

Terminate NAT Gateways

Delete VPC (automatically removes subnets)