<script>
  // TODO: sortDirection for "none"
  // TODO: initialSortKey
  // TODO: initialSortDirection
  // TODO: on:sort event
  // TODO: forward table/pagination events
  // TODO: custom sort logic per column
  // TODO: toolbar? search?

  export let headers = [];
  export let rows = [];
  export let initialSortKey = headers.length > 0 ? headers[1].key : "";
  export let dataTableProps = {};
  export let paginationProps = {};

  export let page = 1;
  export let pageSize = 10;
  export let pageSizes = [pageSize, 50, 100];

  import DataTable from "../DataTable/DataTable.svelte";
  import Pagination from "../Pagination/Pagination.svelte";

  const resolvePath = (object, path, defaultValue) =>
    path
      .split(/[\.\[\]\'\"]/)
      .filter((p) => p)
      .reduce(
        (o, p) => (o && typeof o === "object" && o[p] ? o[p] : defaultValue),
        object
      );

  $: ascending = false;
  $: sortKey = initialSortKey;
  $: headerKeys = headers.map(({ key }) => key);
  $: totalItems = rows.length;
  $: index = pageSize * (page - 1);
  $: normalizedRows = rows.map((row) => ({
    ...row,
    cells: headerKeys.map((key, index) => ({
      key,
      value: resolvePath(row, key, ""),
      display: headers[index].display,
    })),
  }));
  $: sortedRows = [...normalizedRows].sort((a, b) => {
    const itemA = ascending
      ? resolvePath(a, sortKey, "")
      : resolvePath(b, sortKey, "");
    const itemB = ascending
      ? resolvePath(b, sortKey, "")
      : resolvePath(a, sortKey, "");

    // if ($sortHeader.sort) return $sortHeader.sort(itemA, itemB);

    if (typeof itemA === "number" && typeof itemB === "number")
      return itemA - itemB;

    return itemA
      .toString()
      .localeCompare(itemB.toString(), "en", { numeric: true });
  });
  $: currentRows = sortedRows.slice(index, index + pageSize);
</script>

<DataTable
  {...dataTableProps}
  sortable
  headers="{headers}"
  rows="{currentRows}"
  on:click:header="{({ detail }) => {
    ascending = detail.sortDirection === 'ascending';
    sortKey = detail.header.key;
  }}"
/>
<Pagination
  {...paginationProps}
  bind:page
  bind:pageSize
  pageSizes="{pageSizes}"
  totalItems="{totalItems}"
/>
