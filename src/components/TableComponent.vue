<script setup lang="ts">
import {
  FlexRender,
} from "@tanstack/vue-table";

import {
  Table,
  TableBody,
  TableCell,
  TableHead,
  TableHeader,
  TableRow,
} from "@/components/ui/table";



</script>

<template>
  <div class="w-full">
    <div class="border rounded-md">
      <Table>
        <TableHeader>
          <TableRow>
            <TableHead>
              <FlexRender />
            </TableHead>
          </TableRow>
        </TableHeader>
        <TableBody>
          <template>
            <template>
              <TableRow>
                <TableCell>
                  <FlexRender />
                </TableCell>
              </TableRow>
              <TableRow>
                <TableCell>
                  <!-- {{ JSON.stringify(row.original) }} -->
                </TableCell>
              </TableRow>
            </template>
          </template>

          <!-- V-else -->
          <TableRow>
            <TableCell class="h-24 text-center"> No results. </TableCell>
          </TableRow>
        </TableBody>
      </Table>
    </div>
  </div>
</template>
