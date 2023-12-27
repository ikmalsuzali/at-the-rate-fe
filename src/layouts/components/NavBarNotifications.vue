<script setup>
import avatar3 from '@images/avatars/avatar-3.png';
import avatar4 from '@images/avatars/avatar-4.png';
import avatar5 from '@images/avatars/avatar-5.png';
import paypal from '@images/svg/paypal.svg';

const notifications = ref([
{
    id: 1,
    img: avatar4,
    title: 'Task Completed! 🎉',
    subtitle: 'Completed a major project milestone',
    time: 'Today',
    isSeen: true,
  },
  {
    id: 2,
    text: 'Tom Holland',
    title: 'New task assigned.',
    subtitle: 'Assigned 5 hours ago',
    time: 'Yesterday',
    isSeen: false,
  },
  {
    id: 3,
    img: avatar5,
    title: 'Project Update 👋🏻',
    subtitle: 'New project details available',
    time: '11 Aug',
    isSeen: true,
  },
  {
    id: 4,
    img: paypal,
    title: 'Task Deadline Approaching',
    subtitle: 'Task deadline is nearing',
    time: '25 May',
    isSeen: false,
    color: 'error',
  },
  {
    id: 5,
    img: avatar3,
    title: 'Task Assigned 📦',
    subtitle: 'New task assigned from John',
    time: '19 Mar',
    isSeen: true,
  },
])

const removeNotification = notificationId => {
  notifications.value.forEach((item, index) => {
    if (notificationId === item.id)
      notifications.value.splice(index, 1)
  })
}

const markRead = notificationId => {
  notifications.value.forEach(item => {
    notificationId.forEach(id => {
      if (id === item.id)
        item.isSeen = true
    })
  })
}

const markUnRead = notificationId => {
  notifications.value.forEach(item => {
    notificationId.forEach(id => {
      if (id === item.id)
        item.isSeen = false
    })
  })
}

const handleNotificationClick = notification => {
  if (!notification.isSeen)
    markRead([notification.id])
}
</script>

<template>
  <Notifications
    :notifications="notifications"
    @remove="removeNotification"
    @read="markRead"
    @unread="markUnRead"
    @click:notification="handleNotificationClick"
  />
</template>
