<script>
  import { PaginatedDataTable } from "carbon-components-svelte";

  const headers = [
    { key: "name", value: "Name" },
    { key: "protocol", value: "Protocol", sort: false },
    { key: "port", value: "Port" },
    { key: "rule", value: "Rule" },
  ];

  let rows = [
    {
      id: 0,
      name: "Load Balancer 1",
      protocol: "HTTP",
      port: 3000,
      rule: "Round robin",
    },
    {
      id: 1,
      name: "Load Balancer 2",
      protocol: "HTTP",
      port: 443,
      rule: "Round robin",
    },
    {
      id: 2,
      name: "Load Balancer 3",
      protocol: "HTTP",
      port: 80,
      rule: "DNS delegation",
    },
    {
      id: 3,
      name: "Load Balancer 4",
      protocol: "HTTP",
      port: 3030,
      rule: "Round robin",
    },
    {
      id: 4,
      name: "Load Balancer 5",
      protocol: "HTTP",
      port: 443,
      rule: "Round robin",
    },
    {
      id: 5,
      name: "Load Balancer 6",
      protocol: "HTTP",
      port: 80,
      rule: "DNS delegation",
    },
    {
      id: 6,
      name: "Load Balancer 6",
      protocol: "HTTP",
      port: 3000,
      rule: "Round robin",
    },
    {
      id: 7,
      name: "Load Balancer 7",
      protocol: "HTTP",
      port: 443,
      rule: "Round robin",
    },
    {
      id: 8,
      name: "Load Balancer 8",
      protocol: "HTTP",
      port: 80,
      rule: "DNS delegation",
    },
    {
      id: 9,
      name: "Load Balancer 9",
      protocol: "HTTP",
      port: 3000,
      rule: "Round robin",
    },
    {
      id: 10,
      name: "Load Balancer 10",
      protocol: "HTTP",
      port: 443,
      rule: "Round robin",
    },
    {
      id: 11,
      name: "Load Balancer 11",
      protocol: "HTTP",
      port: 80,
      rule: "DNS delegation",
    },
    {
      id: 12,
      name: "Load Balancer 12",
      protocol: "HTTP",
      port: 8000,
      rule: "Round robin",
    },
  ];
</script>

<PaginatedDataTable
  initialSortKey="port"
  dataTableProps="{{
    title: 'Load balancers',
    description: "Your organization's active load balancers.",
  }}"
  headers="{headers}"
  rows="{rows}"
/>
