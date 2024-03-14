<script>
import FullCalendar from '@fullcalendar/vue3'
import dayGridPlugin from '@fullcalendar/daygrid'
import interactionPlugin from '@fullcalendar/interaction'
import timeGridPlugin from '@fullcalendar/timegrid'

export default {
  components: {
    FullCalendar // make the <FullCalendar> tag available
  },
  data() {
    return {
      calendarOptions: {
        plugins: [ dayGridPlugin, interactionPlugin, timeGridPlugin ],
        initialView: 'dayGridMonth',
        selectable: true,
        select: this.selectionInfo,

        //selectionInfo: this.selectionInfo,

        //dateClick: this.handleDateClick,
        events: [
          { title: 'event 1', date: '2024-03-11', color: 'red'},
          { title: 'event 2', date: '2024-03-13', description: 'This is a cool event'},
          //event with description
          { title: 'event 3', date: '2024-03-13', description: 'This is a cool event' },
          //event with url
          { title: 'event 4', date: '2024-03-13', url: 'https://fullcalendar.io' }
        ],
        weekends: true, // initial value
        editable: true,
        droppable: true,
        headerToolbar: {
          left: 'prev,next',
          center: 'title',
          right: 'dayGridMonth,timeGridWeek,timeGridDay' // user can switch between the two
        },
        themeSystem: 'bootstrap5',
        navLinks: true, // can click day/week names to navigate views
        nowIndicator: true, // show a marker for the current date
        businessHours: [{
          // days of week. an array of zero-based day of week integers (0=Sunday)
          daysOfWeek: [ 1, 2, 3, 4, 5 ],
          startTime: '12:00', // a start time (10am in this example)
          endTime: '22:00', // an end time (6pm in this example)
        },
        {
          daysOfWeek: [ 6 ],
          startTime: '8:00', // a start time (10am in this example)
          endTime: '12:00', // an end time (6pm in this example)
        }],

      }
    }
  },
  methods: {
    selectionInfo: function(info) {
      // ask for a title
      let title = prompt('Please enter a new title for your event')
      if (title === null) {
        return
      }
      // add event to calendar
      this.calendarOptions.events = this.calendarOptions.events.concat({ // add new event data
        title: title,
        start: info.startStr,
        end: info.endStr
      })
    },
    handleDateClick: function(arg) {
      alert('date click! ' + arg.dateStr)
    },
  }
}
</script>
<template>
  <link href='https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css' rel='stylesheet'>
  <link href='https://cdn.jsdelivr.net/npm/bootstrap-icons@1.8.1/font/bootstrap-icons.css' rel='stylesheet'>

  <div class="callender">
    <h1>FullCalendar Demo</h1>
    <FullCalendar :options="calendarOptions" />
  </div>
  
</template>
<style>
  .callender {
    width: 80vh;
    height: 100vh;
  }
</style>