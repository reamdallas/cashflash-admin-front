<template>
  <ul
    class="list-group list-group-flush"
    data-toggle="checklist"
  >
    <li
      v-for="item in items"
      :key="item.title"
      class="list-group-item px-0"
    >
      <div
        class="checklist-item"
        :class="{'checklist-item-checked': item.done, [`checklist-item-${item.checkType}`]: item.checkType}"
      >
        <div class="checklist-info">
          <h5 class="checklist-title mb-0">
            {{ item.title }}
          </h5>
          <small>{{ item.description }}</small>
        </div>
        <div>
          <base-checkbox
            v-model="item.done"
            :aria-label="`${item.title} checkbox`"
            :type="item.checkType"
          />
        </div>
      </div>
    </li>
  </ul>
</template>
<script>
export default {
  data() {
    return {
      items: [
        {
          title: 'Call with Dave',
          description: '10:30 AM',
          done: true,
          checkType: 'success',
        },
        {
          title: 'Lunch meeting',
          description: '10:30 AM',
          done: false,
          checkType: 'warning',
        },
        {
          title: 'cashflash Dashboard Launch',
          description: '10:30 AM',
          done: false,
          checkType: 'info',
        },
        {
          title: 'Winter Hackaton',
          description: '10:30 AM',
          done: true,
          checkType: 'danger',
        },
      ],
    };
  },
};
</script>
