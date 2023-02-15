# vue3-type

## types folder

types폴더 안에 타입들을 밀어넣고 익스포트해서 필요한 SFC에서 끌어다가 쓴다

## ref & Type

```jsx
import Job from "./types/Job";
import OrderTerm from "./types/OrderTerm";

const jobList = ref<Job[]>([]);
const order = ref<OrderTerm>("title");
```

## 4-3. props & Type

PropType으로 타입을 던져주자

props의 type은 Vue의 스펙일뿐이다

```jsx
import { defineComponent, PropType, computed } from "vue";
import Job from "@/types/Job";
import OrderTerm from "@/types/OrderTerm";

export default defineComponent({
  props: {
    jobs: {
      required: true,
      type: Array as PropType<Job[]>, // 이건 그냥 뷰의 스펙일뿐 타입스크립트 스펙?이 아니다
    },
    order: {
      required: true,
      type: String as PropType<OrderTerm>,
    },
  },
  setup(props) {
    const orderedJobs = computed(() => {
      return [...props.jobs].sort((a: Job, b: Job) => {
        return a[props.order] > b[props.order] ? 1 : -1;
      });
    });
    return { orderedJobs };
  },
});
```

## 4-4. TS의 타입추론을 믿자

간단한 타입까지 선언하지는 말자
