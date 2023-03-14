<template>
  <div class="modalOverlay">
    <div class="modalContainer">
      <header class="modalHeader">
        <h2 class="modalTitle">H/C RESET STATUS</h2>
      </header>
      <main class="modalMain">
        <div class="lastSession">
          <span>Last Session :</span><span>28 Jun 2019 11:38</span>
        </div>
        <div class="currentStatus">
          <span class="currentStatusText">Current Status :</span>
          <span class="circle currentStatusColor green"></span>
        </div>
        <div class="nextStatus">
          <span class="nextStatusText">New Status : </span>
          <div class="circleContainer">
            <span class="circle green"></span><span class="circle orange"></span
            ><span class="circle red"></span>
          </div>
        </div>
        <div class="comment">
          <span class="commentText">Add a comment :</span>
          <textarea></textarea>
        </div>
        <div class="infoText">
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Iusto harum
          illum velit quisquam? Sed id error reprehenderit?
        </div>
      </main>
      <footer class="modalFooter">
        <div class="buttonsContainer">
          <button>Cancel</button><button>OK</button>
        </div>
      </footer>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.modalOverlay {
  width: 100%;
  height: 100%;
  background-color: rgba(255, 255, 255, 0.6);
  position: absolute;
  z-index: 1000;
  top: 0;
  left: 0;
}
.modalContainer {
  width: 60%;
  height: 60%;
  border: 1px solid black;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
.modalHeader {
  text-align: center;
  height: 15%;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}
.modalMain {
  width: 100%;
  height: 70%;
  background: rgb(255, 255, 255);
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}

.lastSession,
.currentStatus,
.nextStatus {
  margin-left: 3%;
  height: 30px;
}
.currentStatus,
.nextStatus {
  display: flex;
  align-items: center;
}
.currentStatusText,
.nextStatusText,
.commentText {
  width: 30%;
}

.nextStatus .circleContainer {
  display: flex;
  align-items: center;
}
.modalMain .circle {
  display: inline-block;
  height: 30px;
  width: 30px;
  border-radius: 50%;
  margin-left: 20px;
}
.comment {
  display: flex;
  justify-content: center;
  align-items: start;
}
.comment textarea {
  margin-left: 20px;
  flex-grow: 0.8;
}
.infoText {
  width: 95%;
  margin: 0px auto 0px;
}
.modalFooter {
  width: 100%;
  height: 15%;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}
.buttonsContainer {
  width: 50%;
  height: 50%;
  margin-right: 20px;
  display: flex;
  justify-content: flex-end;
}
button {
  width: 30%;
  height: 100%;
  margin-left: 20px;
  border-radius: 50px;
}
.green {
  background: green;
}
.orange {
  background: orange;
}
.red {
  background: red;
}
</style>
