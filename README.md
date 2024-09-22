<p align="center">
    <a href="https://pypi.org/project/streamdeck-sdk-pi" target="_blank">
        <img src="https://img.shields.io/pypi/v/streamdeck-sdk-pi" alt="PyPI">
    </a>
    <a href="https://pypi.org/project/streamdeck-sdk-pi" target="_blank">
        <img src="https://static.pepy.tech/badge/streamdeck-sdk-pi" alt="PyPI">
    </a>
    <a href="https://opensource.org/licenses/Apache-2.0" target="_blank">
        <img src="https://img.shields.io/badge/License-Apache_2.0-blue.svg" alt="Apache">
    </a>
    <a href="https://docs.elgato.com/sdk" target="_blank">
        <img src="https://badgen.net/badge/Elgato/doc/blue" alt="Elgato">
    </a>
</p>

# streamdeck-python-sdk-pi

Library for creating Stream Deck Property Inspector in Python. Write code in Python and get HTML and JS for PI.

**PyPi**: https://pypi.org/project/streamdeck-sdk-pi

**Main project**: https://github.com/gri-gus/streamdeck-python-sdk

**Supported operating systems:**

* MacOS: 10.14 or later
* Windows: 10 or later

**Supported Python versions:** 3.8 or later

## Installation

```shell
pip install streamdeck-sdk-pi
```

## Usage

Look at the `example` folder.

Here are the elements available for generation in Python:

```python
from pathlib import Path

from streamdeck_sdk_pi import *

OUTPUT_DIR = Path(__file__).parent
TEMPLATE = Path(__file__).parent / "pi_template.html"


class LoremFlickrStatus(BasePIElement):
    def get_html_element(self) -> str:
        res = """
    <div class="sdpi-item" style="max-height: 60px">
        <div class="sdpi-item-label">Website status</div>
        <div class="sdpi-item-value"
             style="background: #3D3D3D; height:26px; max-width: 56px; margin: 0 0 0 5px; padding: 0">
            <img src="https://img.shields.io/website?down_color=%233d3d3d&down_message=offline&label=&style=flat-square&up_color=%233d3d3d&up_message=online&url=https%3A%2F%2Floremflickr.com%2F"
                 alt="" style="height: 26px; max-width: 56px; margin: 0">
        </div>
    </div>
        """
        return res


def main():
    pi = PropertyInspector(
        action_uuid="com.ggusev.example.exampleaction",
        elements=[
            Heading(label="TEXT"),
            Textfield(
                label="Name",
                uid="name",
                required=True,
                pattern=".{2,}",
                placeholder="Input your name",
            ),
            Textfield(
                label="Text with default",
                uid="text_with_default",
                placeholder="Input default",
                default_value="default"
            ),
            Textfield(
                label="IP-Address",
                uid="my_ip_address",
                required=True,
                pattern=r"\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}",
                placeholder="e.g. 192.168.61.1",
            ),
            Textarea(
                label="Textarea",
                uid="textarea",
                placeholder="Input",
                max_length=100,
                info_text="100 max"
            ),
            Textarea(label="Textarea", uid="textarea_1", placeholder="Input", ),
            Password(
                label="Password",
                uid="password_input",
                required=True,
                pattern=".{2,}",
                placeholder="Input password",
                default_value="kitten",
            ),
            Heading(label="CHECKBOX & RADIO"),
            Radio(
                label="Union type",
                uid="union_type",
                items=[
                    RadioItem(
                        value="or",
                        label="or",
                        checked=False,
                    ),
                    RadioItem(
                        value="and",
                        label="and",
                        checked=True,
                    )
                ]
            ),
            Checkbox(
                label="Grayscale",
                items=[
                    CheckboxItem(
                        uid="grayscale_flag",
                        label="on",
                        checked=False,
                    ),
                ],
            ),
            Heading(label="FILE"),
            File(
                label="Select file",
                uid="my_file",
                accept=[".jpg", ".jpeg", ".png"],
            ),
            Heading(label="DATE & TIME"),
            DateTimeLocal(
                label="Select datetime",
                uid="my_datetime",
                default_value="2024-09-13T19:39",
            ),
            Date(
                label="Select date",
                uid="my_date",
                default_value="2019-01-15",
            ),
            Date(
                label="Select date",
                uid="my_date_1",
            ),
            Month(
                label="Select month",
                uid="my_month",
                default_value="2024-07",
            ),
            Week(
                label="Select week",
                uid="my_week",
                default_value="2024-W38",
            ),
            Time(
                label="Select time",
                uid="my_time",
                default_value="19:39",
            ),
            Heading(label="GROUP"),
            Group(
                label="My group",
                items=[
                    Radio(
                        label="Union type",
                        uid="my_group_union_type",
                        items=[
                            RadioItem(
                                value="or",
                                label="or",
                                checked=True,
                            ),
                            RadioItem(
                                value="and",
                                label="and",
                                checked=False,
                            )
                        ]
                    ),
                    Date(
                        label="Select date",
                        uid="my_group_my_date",
                        default_value="2019-01-15",
                    ),
                ]
            ),
            Heading(label="LINE"),
            Line(),
            Heading(label="COLOR"),
            Color(
                label="Color",
                uid="my_color",
                default_value="#240bda",
            ),
            Heading(label="PROGRESS & METER"),
            Meter(
                label="Meter",
                uid="my_meter_2",
                default_value=8,
                max_value=100,
            ),
            Meter(
                label="Meter",
                uid="my_meter_1",
                default_value=0.5,
                left_label="0",
                right_label="100",
            ),
            Progress(
                label="Progress",
                uid="my_progress_1",
                default_value=0.5,
            ),
            Progress(
                label="Progress",
                uid="my_progress_2",
                left_label="Min",
                right_label="Max",
                default_value=0.5,
            ),
            Heading(label="RANGE"),
            Range(
                label="Range",
                uid="my_range_2",
                min_value=0,
                max_value=50,
                default_value=20,
            ),
            Range(
                label="Range (+ll + rl)",
                uid="my_range_1",
                left_label="0",
                right_label="50",
                min_value=0,
                max_value=50,
                default_value=20,
            ),
            Range(
                label="Range(+stp)",
                uid="my_range_3",
                min_value=0,
                max_value=50,
                default_value=25,
                step=25,
            ),
            Range(
                label="Range(+dl +stp)",
                uid="my_range_4",
                min_value=0,
                max_value=50,
                default_value=25,
                datalist=["", "", "", ],
                step=25,
            ),
            Range(
                label="Range(+dl +lbl)",
                uid="my_range_5",
                min_value=0,
                max_value=100,
                default_value=25,
                datalist=["0", "50", "100", ],
            ),
            Heading(label="DETAILS"),
            Details(
                uid="my_full_width_details",
                full_width=True,
                heading="Full width details",
                text="""
                default open
                """,
                default_open=True,
            ),
            Details(
                uid="my_details_with_label",
                label="Details",
                heading="Info",
                text="My test info\nMy test info"
            ),
            Heading(label="MESSAGE"),
            Message(
                uid="my_message",
                heading="Example message",
                message_type=MessageTypes.INFO,
                text="Example message text",
            ),
            Message(
                uid="last_error",
                heading="Last error",
                message_type=MessageTypes.CAUTION,
                text="",
            ),
            Heading(label="SELECT"),
            Select(
                uid="my_select_1",
                label="Select",
                values=["1", "2", "3", "4"],
                default_value="2",
            ),
            Select(
                uid="my_select_2",
                label="Select 2",
                values=[],
            ),
            Heading(label="CUSTOM"),
            LoremFlickrStatus(),
        ]
    )
    pi.build(output_dir=OUTPUT_DIR, template=TEMPLATE)


if __name__ == '__main__':
    main()

```

> You can write your custom elements, for example as `LoremFlickrStatus`, and also edit `pi_template.html`
> at your discretion.

> `uid` is a future key in the `obj.payload.settings` dictionary.

> The same rules apply to `uid` as to variable naming in Python.

> `uid` must be unique within a single file for Property Inspector generation.

> All elements that contain `uid` are manipulable.