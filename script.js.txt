function login() {
    const username = document.getElementById('username').value;
    const password = document.getElementById('password').value;

    if (username === 'Ajay' && password === '123456') {
        document.getElementById('loginPage').classList.add('hidden');
        document.getElementById('actionPage').classList.remove('hidden');
    } else {
        document.getElementById('loginError').style.display = 'block';
    }
}

function selectAction(action) {
    document.getElementById('actionPage').classList.add('hidden');
    if (action === 'event') {
        document.getElementById('eventPage').classList.remove('hidden');
    } else if (action === 'complaint') {
        document.getElementById('complaintPage').classList.remove('hidden');
    }
}

document.getElementById('eventForm').addEventListener('submit', function(event) {
    event.preventDefault();
    const title = document.getElementById('eventTitle').value;
    const date = document.getElementById('eventDate').value;
    const time = document.getElementById('eventTime').value;
    const location = document.getElementById('eventLocation').value;
    const description = document.getElementById('eventDescription').value;

    const eventItem = document.createElement('div');
    eventItem.classList.add('event-item');
    eventItem.innerHTML = `
        <div class="event-title">${title}</div>
        <div class="event-details">
            <p>Date: ${date}</p>
            <p>Time: ${time}</p>
            <p>Location: ${location}</p>
            <p>Description: ${description}</p>
        </div>
    `;
    document.getElementById('eventList').appendChild(eventItem);
    document.getElementById('eventForm').reset();
});

document.getElementById('complaintForm').addEventListener('submit', function(event) {
    event.preventDefault();
    const title = document.getElementById('complaintTitle').value;
    const description = document.getElementById('complaintDescription').value;
    const photo = document.getElementById('complaintPhoto').files[0];
    const photoURL = photo ? URL.createObjectURL(photo) : '';

    const complaintItem = document.createElement('div');
    complaintItem.classList.add('complaint-item');
    complaintItem.innerHTML = `
        <div class="complaint-title">${title}</div>
        <div class="complaint-details">
            <p>Description: ${description}</p>
            ${photo ? `<img src="${photoURL}" class="complaint-photo" alt="Complaint photo">` : ''}
        </div>
    `;
    document.getElementById('complaintList').appendChild(complaintItem);
    document.getElementById('complaintForm').reset();
    document.getElementById('photoPreview').style.display = 'none';
});

function markDone(taskType) {
    if (taskType === 'event') {
        document.getElementById('eventDoneMessage').classList.remove('hidden');
    } else if (taskType === 'complaint') {
        document.getElementById('complaintDoneMessage').classList.remove('hidden');
    }
}

function goBack(page) {
    if (page === 'action') {
        document.getElementById('eventPage').classList.add('hidden');
        document.getElementById('complaintPage').classList.add('hidden');
        document.getElementById('actionPage').classList.remove('hidden');
    }
}

function previewImage(event) {
    const reader = new FileReader();
    reader.onload = function () {
        const output = document.getElementById('photoPreview');
        output.src = reader.result;
        output.style.display = 'block';
    }
    reader.readAsDataURL(event.target.files[0]);
}
